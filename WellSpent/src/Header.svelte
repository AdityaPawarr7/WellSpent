<script>
  export let title = "WellSpent";
  export let sensorStatus = "Connected";
</script>

<header>
  <div class="brand">
    <h1>{title}</h1>
  </div>
  
  <div class="status">
    <span class="dot" class:active={sensorStatus === "Connected"}></span>
    <span class="status-text">Sensor {sensorStatus}</span>
  </div>
</header>

<style>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 0;
    margin-bottom: 1rem;
    border-bottom: 1px solid var(--border);
  }

  h1 {
    margin: 0;
    font-size: 1.5rem;
    color: var(--primary);
  }

  .status {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.85rem;
    color: var(--text-muted);
  }

  .dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: #ef4444; /* Red by default */
    box-shadow: 0 0 5px #ef4444;
  }

  .dot.active {
    background-color: #22c55e; /* Green for connected */
    box-shadow: 0 0 5px #22c55e;
  }
</style>