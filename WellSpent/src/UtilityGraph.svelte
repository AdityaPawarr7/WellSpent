<script>
  // Mock Data: Stacked or multi-line simulation
  // Showing simplified "This Month" breakdown for clarity in small space
  let utilities = [
    { name: 'Shower', val: 45, color: '#3b82f6' },
    { name: 'Sprinkler', val: 30, color: '#22c55e' },
    { name: 'Tap', val: 15, color: '#fbbf24' },
    { name: 'Dishwasher', val: 10, color: '#a855f7' }
  ];
</script>

<div class="graph-card">
  <h4>Utility Breakdown</h4>
  
  <div class="bars-container">
    {#each utilities as u}
      <div class="utility-row">
        <div class="u-info">
          <span class="u-dot" style="background: {u.color}"></span>
          <span class="u-name">{u.name}</span>
        </div>
        <div class="u-track">
          <div class="u-bar" style="width: {u.val}%; background: {u.color}"></div>
        </div>
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
    pointer-events: none;
  }
  
  h4 { margin: 0 0 1rem 0; font-size: 0.9rem; color: var(--text-muted); }

  .bars-container { display: flex; flex-direction: column; gap: 0.8rem; }

  .utility-row { display: flex; align-items: center; gap: 0.5rem; font-size: 0.8rem; }
  
  .u-info { width: 90px; display: flex; align-items: center; gap: 6px; color: var(--text-muted); }
  .u-dot { width: 8px; height: 8px; border-radius: 50%; }

  .u-track { flex: 1; height: 6px; background: rgba(255,255,255,0.05); border-radius: 3px; overflow: hidden; }
  .u-bar { height: 100%; border-radius: 3px; }
</style>