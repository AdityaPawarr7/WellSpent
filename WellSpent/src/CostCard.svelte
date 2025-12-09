<script>
  export let expected = 0;
  export let target = 0;
  
  // Calculate if over budget
  $: isOver = expected > target;
</script>

<div class="card" class:warning={isOver}>
  <div class="metric">
    <span class="label">Expected Cost</span>
    <span class="value">${expected.toFixed(2)}</span>
  </div>
  
  <div class="divider"></div>

  <div class="metric">
    <span class="label">Target Cost</span>
    <span class="value target">${target.toFixed(2)}</span>
  </div>
</div>

<style>
  .card {
    background-color: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.5rem;
    display: inline-flex;
    justify-content: space-around;
    align-items: center;
    margin-bottom: 1.5rem;
    transition: 0.3s;
  }

  /* Red border glow if over budget */
  .card.warning {
    border-color: #ef4444;
    box-shadow: 0 0 10px rgba(239, 68, 68, 0.1);
  }

  .metric {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .label {
    font-size: 0.8rem;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin-bottom: 0.25rem;
  }

  .value {
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--text-main);
  }

  .value.target {
    color: var(--primary);
  }

  .divider {
    width: 1px;
    height: 40px;
    background-color: var(--border);
  }
</style>