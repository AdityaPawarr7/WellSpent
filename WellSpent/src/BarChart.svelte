<script>
  export let data = [];
  export let limit = 100;
  export let label = "Usage History";

  // Calculate chart scale
  $: maxVal = Math.max(...data, limit * 1.2); 
</script>

<div class="chart-container">
  <h4>{label}</h4>
  
  <div class="chart">
    <div class="limit-line" style="bottom: {(limit / maxVal) * 100}%;">
      <span>Limit: {limit}L</span>
    </div>

    {#each data as value}
      {@const height = (value / maxVal) * 100}
      {@const isOver = value > limit}
      
      <div class="bar-wrapper">
        <div class="bar" class:over={isOver} style="height: {height}%;"></div>
      </div>
    {/each}
  </div>
</div>

<style>
  .chart-container {
    margin-top: 1rem;
    padding: 1.5rem;
    background: var(--bg-card);
    border-radius: 12px;
    border: 1px solid var(--border);
  }

  h4 { margin: 0 0 1.5rem 0; color: var(--text-muted); font-weight: 500; font-size: 0.9rem;}

  .chart {
    height: 120px;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    position: relative;
    padding-top: 1rem;
  }

  .limit-line {
    position: absolute;
    left: 0;
    right: 0;
    border-top: 1px dashed #ef4444;
    z-index: 2;
    opacity: 0.8;
  }

  .limit-line span {
    position: absolute;
    right: 0;
    top: -18px;
    font-size: 0.7rem;
    color: #ef4444;
  }

  .bar-wrapper {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: flex-end;
    justify-content: center;
    padding: 0 4px;
  }

  .bar {
    width: 100%;
    background-color: #4ade80; /* Nice Green */
    border-radius: 4px 4px 0 0;
    min-height: 4px;
  }

  .bar.over {
    background: linear-gradient(to top, #4ade80 50%, #ef4444); /* Green to Red fade */
  }
</style>