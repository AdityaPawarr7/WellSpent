<script>
  export let isOver = false;
</script>

<div class="scenery" class:drought={isOver}>
  <div class="sky">
    {#if isOver}
      <div class="sun harsh"></div>
    {:else}
      <div class="cloud"></div>
      <div class="sun"></div>
    {/if}
  </div>
  
  <div class="ground">
    <div class="tree-container">
      {#if isOver}
        <span class="icon">🍂</span>
        <p class="status-text">Drought Warning</p>
      {:else}
        <span class="icon">🌳</span>
        <p class="status-text">Healthy Levels</p>
      {/if}
    </div>
  </div>
</div>

<style>
  .scenery {
    height: 180px;
    border-radius: 12px;
    overflow: hidden;
    position: relative;
    display: flex;
    flex-direction: column;
    margin-bottom: 1.5rem;
    border: 2px solid var(--border);
    transition: 0.5s;
  }

  /* --- Healthy State (Default) --- */
  .scenery {
    background: linear-gradient(to bottom, #60a5fa, #bfdbfe); /* Blue Sky */
  }
  .ground {
    height: 30%;
    background-color: #22c55e; /* Green Grass */
    width: 100%;
    margin-top: auto;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    padding-bottom: 10px;
  }

  /* --- Drought State (Over Budget) --- */
  .scenery.drought {
    background: linear-gradient(to bottom, #fbbf24, #fef3c7); /* Hot Yellow Sky */
    border-color: #ef4444;
  }
  .scenery.drought .ground {
    background-color: #d97706; /* Dry Dirt */
  }

  /* --- Elements --- */
  .tree-container {
    text-align: center;
    z-index: 2;
  }
  .icon {
    font-size: 3rem;
    display: block;
    filter: drop-shadow(0 4px 4px rgba(0,0,0,0.2));
  }
  .status-text {
    margin: 0;
    font-size: 0.8rem;
    font-weight: bold;
    color: white;
    text-shadow: 0 1px 2px rgba(0,0,0,0.5);
    background: rgba(0,0,0,0.3);
    padding: 2px 8px;
    border-radius: 10px;
  }

  /* Simple Sun/Cloud animations could go here */
  .sun {
    position: absolute;
    top: 20px;
    right: 20px;
    width: 40px;
    height: 40px;
    background: #fde047;
    border-radius: 50%;
    box-shadow: 0 0 20px #fde047;
  }
</style>