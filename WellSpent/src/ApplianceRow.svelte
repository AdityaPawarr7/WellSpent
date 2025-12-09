<script>
  import Icon from './Icon.svelte'; // Import the new Icon component

  export let name = "Appliance";
  export let icon = "tap"; // Default icon
  export let usage = 0;
  export let target = 0;

  $: percent = Math.min((usage / target) * 100, 100);
  $: isOver = usage > target;
</script>

<div class="row">
  <div class="icon-circle">
    <Icon name={icon} size="24" color="var(--primary)" />
  </div>

  <div class="info">
    <h3>{name}</h3>
    <div class="stats">
      <span class:danger={isOver}>{usage}L</span>
      <span class="target"> / {target}L</span>
    </div>
  </div>

  <div class="actions">
    <button class="btn-icon">
       <Icon name="graph" size="18" />
    </button>
    <button class="btn-icon">
       <Icon name="edit" size="18" />
    </button>
  </div>
</div>

<div class="progress-bar">
  <div class="fill" style="width: {percent}%; background-color: {isOver ? '#ef4444' : '#22c55e'};"></div>
</div>

<style>
  .row {
    display: flex;
    align-items: center;
    padding: 1rem 0 0.5rem 0;
    gap: 1rem; /* Space between icon and text */
  }

  .icon-circle {
    width: 40px;
    height: 40px;
    background: rgba(59, 130, 246, 0.1);
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .info { flex: 1; } /* Pushes the buttons to the right */

  h3 { margin: 0; font-size: 1rem; }
  
  .stats { font-size: 0.85rem; color: var(--text-muted); }
  .danger { color: #ef4444; font-weight: bold; }

  .actions { display: flex; gap: 0.5rem; }
  
  .btn-icon {
    background: var(--bg-card);
    border: 1px solid var(--border);
    padding: 0.4rem;
    border-radius: 6px;
    cursor: pointer;
    color: var(--text-muted);
  }
  .btn-icon:hover { color: var(--text-main); border-color: var(--primary); }

  .progress-bar {
    height: 4px;
    background: #333;
    border-radius: 2px;
    margin-bottom: 1rem;
    overflow: hidden;
  }
  .fill { height: 100%; transition: width 0.5s; }
</style>