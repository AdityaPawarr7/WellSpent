<script>
  export let data = []; 
  const maxVal = 2.0; 
</script>

<div class="graph-card">
  <div class="header">
    <h4>Live Water Flow</h4>
    <span class="live-indicator">
      <span class="dot"></span> LIVE
    </span>
  </div>
  
  <div class="chart">
    {#each data as value, i}
      <div class="bar-wrapper">
        <div 
          class="bar" 
          style="height: {Math.max((value / maxVal) * 100, 2)}%; opacity: {(i + 5) / data.length}"
        ></div>
      </div>
    {/each}
  </div>
</div>

<style>
  .graph-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.5rem;
    margin-bottom: 1rem;
    /* Removed flex properties */
  }
  
  .header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem; }
  h4 { margin: 0; font-size: 0.9rem; color: var(--text-muted); }

  .live-indicator { font-size: 0.7rem; font-weight: bold; color: #ef4444; display: flex; align-items: center; gap: 4px; }
  .dot { width: 6px; height: 6px; background: #ef4444; border-radius: 50%; animation: pulse 1s infinite; }

  .chart {
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
    gap: 3px;
    overflow: hidden;
    
    /* REVERTED: Fixed height */
    height: 100px;
    width: 100%;
  }

  .bar-wrapper { flex: 1; height: 100%; display: flex; align-items: flex-end; }
  
  .bar {
    width: 100%;
    background: var(--primary);
    border-radius: 2px;
    transition: height 0.2s ease;
  }

  @keyframes pulse {
    0% { opacity: 1; }
    50% { opacity: 0.4; }
    100% { opacity: 1; }
  }
</style>