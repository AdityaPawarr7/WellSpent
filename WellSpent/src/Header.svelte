<script>
  import { createEventDispatcher } from 'svelte';
  export let activePage = 'dashboard';
  
  const dispatch = createEventDispatcher();
</script>

<header>
  
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <div class="brand" on:click={() => dispatch('nav', 'dashboard')}>
    <span class="logo">🚰</span>
    <span class="title">WellSpent</span>
  </div>

  <nav>
    <button 
      class:active={activePage === 'dashboard'} 
      on:click={() => dispatch('nav', 'dashboard')}
    >
      Dashboard
    </button>
    <button 
      class:active={activePage === 'history'} 
      on:click={() => dispatch('nav', 'history')}
    >
      View History
    </button>
    <button 
      class:active={activePage === 'donate'} 
      on:click={() => dispatch('nav', 'donate')}
    >
      Pay / Donate
    </button>
  </nav>

  <div class="profile">
    <span class="username">Aditya Pawar</span>
    <div class="avatar">AP</div>
  </div>
</header>

<style>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.75rem 1.5rem;
    background-color: var(--bg-card);
    border-bottom: 1px solid var(--border);
    margin-bottom: 2rem;
  }

  .brand { 
    display: flex; align-items: center; gap: 0.5rem; 
    font-weight: bold; font-size: 1.2rem; cursor: pointer; 
  }
  
  nav { display: flex; gap: 1rem; }
  
  button {
    background: transparent;
    border: none;
    color: var(--text-muted);
    font-weight: 500;
    cursor: pointer;
    font-size: 0.95rem;
    padding: 0.5rem 1rem;
    border-radius: 6px;
    transition: 0.2s;
  }

  button:hover { color: var(--text-main); background: rgba(255,255,255,0.05); }
  button.active { color: var(--primary); background: rgba(59, 130, 246, 0.1); }

  .profile { display: flex; align-items: center; gap: 0.8rem; }
  .username { font-weight: 600; font-size: 0.95rem; }

  .avatar {
    width: 36px; height: 36px;
    background-color: var(--primary);
    color: rgb(0, 0, 0);
    font-weight: bold;
    font-size: 0.85rem;
    border-radius: 50%;
    cursor: pointer;
    display: flex; justify-content: center; align-items: center;
  }
  .title {
    font-size: larger;
  }
</style>