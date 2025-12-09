<script>
  // Mock Data for the last 12 months
  let history = [
    { m: 'J', val: 80 }, { m: 'F', val: 75 }, { m: 'M', val: 90 }, 
    { m: 'A', val: 110 }, { m: 'M', val: 130 }, { m: 'J', val: 160 }, 
    { m: 'J', val: 180 }, { m: 'A', val: 170 }, { m: 'S', val: 140 }, 
    { m: 'O', val: 100 }, { m: 'N', val: 90 }, { m: 'D', val: 85 }
  ];
  const max = 200; // Scale max
</script>

<div class="graph-card">
  <h4>Total Usage (12 Mo)</h4>
  <div class="chart">
    {#each history as item}
      <div class="bar-group">
        <div class="bar" style="height: {(item.val / max) * 100}%"></div>
        <span class="label">{item.m}</span>
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
    pointer-events: none; /* Let parent handle click */
  }
  
  h4 { margin: 0 0 1rem 0; font-size: 0.9rem; color: var(--text-muted); }

  .chart {
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    height: 100px;
    gap: 4px;
  }

  .bar-group {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    justify-content: flex-end;
    flex: 1;
  }

  .bar {
    width: 6px;
    background: var(--primary);
    border-radius: 3px;
    opacity: 0.8;
  }

  .label {
    margin-top: 6px;
    font-size: 0.6rem;
    color: var(--text-muted);
  }
</style>