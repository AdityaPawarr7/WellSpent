<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  
  function navigate(page) {
    dispatch('nav', page);
  }
</script>

<div class="grid">
  <button class="nav-card" on:click={() => navigate('usage')}>
    <span class="icon">💧</span>
    <span class="label">Add Usage</span>
  </button>

  <button class="nav-card" on:click={() => navigate('limits')}>
    <span class="icon">⚙️</span>
    <span class="label">Set Limits</span>
  </button>

  <button class="nav-card full-width" on:click={() => navigate('donate')}>
    <span class="icon">🤝</span>
    <span class="label">Donate</span>
  </button>
</div>

<style>
  .grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    margin-bottom: 1.5rem;
  }
  
  .nav-card {
    background-color: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
    transition: 0.2s;
    color: var(--text-main);
  }

  .full-width {
    grid-column: span 2;
  }

  .nav-card:hover {
    background-color: #2a2a2a;
    border-color: var(--primary);
  }

  .icon { font-size: 1.5rem; }
  .label { font-weight: 600; }
</style>