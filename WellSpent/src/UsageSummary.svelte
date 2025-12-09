<script>
  import { createEventDispatcher } from 'svelte';
  export let usage = 1240.02;
  export let limit = 1000; // Pass in the limit so we can see it

  const dispatch = createEventDispatcher();
</script>

<div class="summary-card">
  <div class="header-row">
    <h3>Water Usage <span class="sub">This Month</span></h3>
    <button class="edit-btn" on:click={() => dispatch('edit')} title="Edit Limit">
      ✏️
    </button>
  </div>
  
  <div class="metric-container">
    <span class="big-number" class:danger={usage > limit}>{usage}</span>
    <span class="unit">Lts</span>
  </div>
  
  <div class="limit-display">
    Target: {limit} Lts
  </div>
</div>

<style>
  .summary-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 2.5rem;
    text-align: center;
    position: relative;
  }
  
  .header-row {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 0.5rem;
    margin-bottom: 0.5rem;
  }

  h3 { 
    font-size: 1rem; 
    margin: 0; 
    color: var(--text-muted); 
    text-transform: uppercase; 
    letter-spacing: 0.05em;
  }
  .sub { color: var(--text-muted); font-weight: 400; opacity: 0.7; }

  .edit-btn {
    background: transparent;
    border: none;
    cursor: pointer;
    font-size: 0.9rem;
    opacity: 0.5;
    transition: 0.2s;
    padding: 2px;
  }
  .edit-btn:hover { opacity: 1; transform: scale(1.1); }

  .metric-container {
    display: flex; justify-content: center; align-items: baseline; gap: 0.5rem;
  }

  .big-number { font-size: 2.5rem; font-weight: 800; color: var(--text-main); transition: 0.3s; }
  .big-number.danger { color: #ef4444; } /* Red if over limit */
  
  .unit { font-size: 1.2rem; color: var(--primary); font-weight: 600; }
  
  .limit-display { font-size: 0.85rem; color: var(--text-muted); margin-top: 0.5rem; }
</style>