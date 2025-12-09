<script>
  import Header from './Header.svelte';
  import CostCard from './CostCard.svelte';
  import Scenery from './Scenery.svelte';
  import NavGrid from './NavGrid.svelte';
  import ApplianceRow from './ApplianceRow.svelte';
  import BarChart from './BarChart.svelte';

  // --- STATE ---
  let currentPage = 'dashboard'; // Options: 'dashboard', 'usage', 'limits', 'donate'
  
  // Mock Data
  let costData = {
    expected: 45.50,
    target: 40.00
  };

  // Derived state for the scenery
  $: isOverBudget = costData.expected > costData.target;

  // --- NAVIGATION HANDLER ---
  function handleNav(event) {
    currentPage = event.detail;
  }
  
  function goHome() {
    currentPage = 'dashboard';
  }
</script>

<main class="container">
  <Header title="WellSpent" sensorStatus="Connected" />

  {#if currentPage === 'dashboard'}
    <CostCard 
      expected={costData.expected} 
      target={costData.target} 
    />

    <Scenery isOver={isOverBudget} />

    <NavGrid on:nav={handleNav} />

{:else if currentPage === 'limits'}
    <div class="sub-page">
      <button class="back-btn" on:click={goHome}>← Back</button>
      <h2>Set Appliance Limits</h2>
      
      <div class="list">
        <ApplianceRow 
          name="Master Shower" 
          icon="shower" 
          usage={120} 
          target={100} 
        />
        <ApplianceRow 
          name="Guest Shower" 
          icon="shower" 
          usage={40} 
          target={80} 
        />
        <ApplianceRow 
          name="Dishwasher" 
          icon="dishwasher" 
          usage={94} 
          target={90} 
        />
        <ApplianceRow 
          name="Lawn Sprinklers" 
          icon="lawn" 
          usage={200} 
          target={150} 
        />
      </div>

      <BarChart 
        label="Master Shower History" 
        limit={100} 
        data={[80, 90, 110, 130, 95, 100, 105]} 
      />
    </div>

  {:else if currentPage === 'usage'}
    <div class="sub-page">
      <button class="back-btn" on:click={goHome}>← Back</button>
      <h2>Add Water Usage</h2>
      <p>Manual entry form goes here...</p>
    </div>

  {:else if currentPage === 'donate'}
    <div class="sub-page">
      <button class="back-btn" on:click={goHome}>← Back</button>
      <h2>Donate to Non-Profits</h2>
      <p>Conservation resources...</p>
    </div>

  {/if}

</main>

<style>
  .container {
    max-width: 480px;
    margin: 0 auto;
    padding: 1rem;
    min-height: 100vh;
  }
  
  .sub-page {
    animation: fadeIn 0.3s ease;
  }

  .back-btn {
    background: transparent;
    border: 1px solid var(--border);
    color: var(--text-muted);
    margin-bottom: 1rem;
    padding: 0.4rem 0.8rem;
  }
  
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(5px); }
    to { opacity: 1; transform: translateY(0); }
  }
</style>