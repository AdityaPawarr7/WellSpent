<script>
  import { createEventDispatcher } from 'svelte';
  export let activePage = 'dashboard';
  
  const dispatch = createEventDispatcher();
</script>

<header>
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
    <div class="avatar">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" width="20" height="20">
        <path fill-rule="evenodd" d="M7.5 6a4.5 4.5 0 119 0 4.5 4.5 0 01-9 0zM3.751 20.105a8.25 8.25 0 0116.498 0 .75.75 0 01-.437.695A18.683 18.683 0 0112 22.5c-2.786 0-5.433-.608-7.812-1.7a.75.75 0 01-.437-.695z" clip-rule="evenodd" />
      </svg>
    </div>
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
    color: white;
    border-radius: 50%;
    cursor: pointer;
    display: flex; justify-content: center; align-items: center;
  }
</style>