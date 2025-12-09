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
        <p class="status-text warning">Drought Warning</p>
      {:else}
        <span class="icon">🌳</span>
        <p class="status-text">Healthy Levels</p>
      {/if}
    </div>
  </div>
</div>

<style>
  .scenery {
   
    height: 250px;
    
    border-radius: 12px;
    overflow: hidden;
    position: relative;
    display: flex;
    flex-direction: column;
    margin-bottom: 1.5rem;
    border: 1px solid var(--border);
    transition: 0.5s;
    background: linear-gradient(to bottom, #60a5fa, #bfdbfe);
  }

  .ground {
    height: 30%;
    background-color: #22c55e;
    width: 100%;
    margin-top: auto;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    padding-bottom: 10px;
    transition: 0.5s;
  }

  /* Drought State */
  .scenery.drought {
    background: linear-gradient(to bottom, #fbbf24, #fef3c7);
    border-color: #ef4444;
  }
  .scenery.drought .ground { background-color: #d97706; }

  /* Elements */
  .tree-container { text-align: center; z-index: 2; }
  .icon { font-size: 3rem; display: block; filter: drop-shadow(0 4px 4px rgba(0,0,0,0.2)); transition: 0.3s; }
  
  .status-text {
    margin: 0; font-size: 0.85rem; font-weight: bold; color: white;
    text-shadow: 0 1px 2px rgba(0,0,0,0.5);
    background: rgba(0,0,0,0.3); padding: 4px 10px; border-radius: 12px;
  }
  .status-text.warning { background: #ef4444; }

  /* Sun Animation */
  .sun {
    position: absolute; top: 20px; right: 20px;
    width: 40px; height: 40px; /* Smaller sun */
    background: #fde047; border-radius: 50%;
    box-shadow: 0 0 20px #fde047;
  }
</style>