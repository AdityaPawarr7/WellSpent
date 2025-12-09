<script>
  import { createEventDispatcher } from 'svelte';
  
  // Now accepts the whole device object
  export let device = { name: 'Unknown', isOn: false };

  const dispatch = createEventDispatcher();

  function toggle(state) {
    // Tell App.svelte to update this device
    dispatch('toggle', { id: device.id, state: state });
  }
</script>

<div class="control-card">
  <h3>{device.name}</h3>
  
  <div class="status-display">
    <span class="shower-icon" class:active={device.isOn}>🚿</span>
    <div class="status-text">
      Status: <span style="color: {device.isOn ? '#22c55e' : '#ef4444'}">
        {device.isOn ? 'ON' : 'OFF'}
      </span>
    </div>
  </div>

  <div class="buttons">
    <button class="btn start" disabled={device.isOn} on:click={() => toggle(true)}>Start</button>
    <button class="btn stop" disabled={!device.isOn} on:click={() => toggle(false)}>Stop</button>
  </div>
</div>

<style>
  .control-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.5rem;
    text-align: center;
    height: 100%;
    display: flex; flex-direction: column; justify-content: space-between;
  }

  h3 { margin-top: 0; font-size: 1.4rem;}

  .status-display { margin: 1rem 0; }
  .shower-icon { font-size: 4rem; display: block; filter: grayscale(100%); transition: 0.3s; margin-bottom: 0.5rem; opacity: 0.5; }
  .shower-icon.active { filter: grayscale(0%); opacity: 1; transform: scale(1.1); }
  
  .status-text { font-weight: bold; font-size: 1.1rem; }

  .buttons { display: flex; gap: 1rem; margin-top: auto; }
  .btn { flex: 1; padding: 0.8rem; font-weight: bold; border-radius: 8px; border: none; cursor: pointer; transition: 0.2s; }
  
  .start { background: rgba(34, 197, 94, 0.2); color: #22c55e; }
  .start:hover:not(:disabled) { background: rgba(34, 197, 94, 0.4); }
  
  .stop { background: rgba(239, 68, 68, 0.2); color: #ef4444; }
  .stop:hover:not(:disabled) { background: rgba(239, 68, 68, 0.4); }

  button:disabled { opacity: 0.3; cursor: not-allowed; }
</style>