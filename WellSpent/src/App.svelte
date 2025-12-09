<script>
// @ts-nocheck

  import { onMount, onDestroy } from 'svelte';
  import Header from './Header.svelte';
  import Scenery from './Scenery.svelte';
  import CostCard from './CostCard.svelte';
  import DeviceControl from './DeviceControl.svelte';
  import UsageSummary from './UsageSummary.svelte';
  import MasterGraph from './MasterGraph.svelte';
  import UtilityGraph from './UtilityGraph.svelte';
  import LiveGraph from './LiveGraph.svelte';

  // Cost per Liter usage in dollars.
  const COST_PER_LITER = 0.05; 
  
  // Icons for different utility types
  const iconMap = {
    shower: '🚿', 
    tap: '💧',       
    lawn: '⛲',      
    dishwasher: '🍽️', 
    toilet: '🚽', 
    washer: '🫧'     
  };

  // state of the application on startup
  let currentPage = 'dashboard'; 
  
  let devices = [
    { id: 1, name: "Master Shower", type: 'shower', limit: 100, usage: 45.5, isOn: false },
    { id: 2, name: "Kitchen Sink", type: 'tap', limit: 50, usage: 12.0, isOn: false },
    { id: 3, name: "Garden Sprinklers", type: 'lawn', limit: 200, usage: 180.0, isOn: false },
    { id: 4, name: "Dishwasher", type: 'dishwasher', limit: 30, usage: 30.0, isOn: false },

  ];

  let selectedId = 1;
  let showAddModal = false; 
  let showLimitModal = false;
  let globalLimit = 200; 

  // Live Graph State
  let flowHistory = new Array(30).fill(0); 

  // reactive declarations
  $: activeDevice = devices.find(d => d.id === selectedId) || devices[0];
  $: totalUsage = devices.reduce((sum, d) => sum + d.usage, 0);
  $: totalLimit = globalLimit; 
  $: totalCost = (totalUsage * COST_PER_LITER); 
  $: targetCost = (totalLimit * COST_PER_LITER);
  $: isOverBudget = totalUsage > totalLimit;
  
  $: overageAmount = Math.max(0, totalUsage - totalLimit);
  $: donationSuggestion = overageAmount * COST_PER_LITER;

  // simulating live data updates
  let interval;
  onMount(() => {
    interval = setInterval(() => {
      let currentTickFlow = 0; 

      devices = devices.map(d => {
        if (d.isOn) {
          // Simulate flow rate between 0.1 to 0.5 L/s
          const flow = (Math.random() * 0.4 + 0.1);
          currentTickFlow += flow; 
          return { ...d, usage: d.usage + flow };
        }
        return d;
      });

      // Update live graph data
      flowHistory = [...flowHistory.slice(1), currentTickFlow];
    }, 1000); 
  });

  onDestroy(() => clearInterval(interval));
  

  // event handlers
  function handleToggle(event) {
    const { id, state } = event.detail;
    devices = devices.map(d => d.id === id ? { ...d, isOn: state } : d);
  }

  function handleAddDevice(event) {
    event.preventDefault();
    const formData = new FormData(event.target);
    const newDevice = {
      id: Date.now(),
      name: formData.get('name'),
      type: formData.get('type'),
      // @ts-ignore
      limit: parseFloat(formData.get('limit')),
      usage: 0,
      isOn: false
    };
     // @ts-ignore
    devices = [...devices, newDevice];
    selectedId = newDevice.id;
    showAddModal = false;
  }

  function handleUpdateLimit(event) {
    event.preventDefault();
    const formData = new FormData(event.target);
     // @ts-ignore
    globalLimit = parseFloat(formData.get('limit'));
    showLimitModal = false;
  }

  function handleNav(event) {
    currentPage = event.detail;
    window.scrollTo(0,0);
  }
</script>

<div class="app-container">
  
  <Header activePage={currentPage} on:nav={handleNav} />

  {#if currentPage === 'dashboard'}
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <main class="dashboard-grid fade-in">
    
    <div class="col-left">
      <div class="top-group">
        <Scenery isOver={isOverBudget} />
        <UsageSummary 
          usage={totalUsage.toFixed(2)} 
          limit={totalLimit} 
          on:edit={() => showLimitModal = true} 
        />
      </div>
      <CostCard expected={totalCost} target={targetCost} />
    </div>

    <div class="col-center">
      <DeviceControl device={activeDevice} on:toggle={handleToggle} />
      
      <div class="utility-manager">
        <div class="manager-header">
          <h3>My Utilities</h3>
          <button class="master-add-btn" on:click={() => showAddModal = true}>
            + Add Utility
          </button>
        </div>
        
        <div class="device-list">
          {#each devices as dev}
            <button 
              class="device-item" 
              class:selected={selectedId === dev.id}
              class:running={dev.isOn}
              on:click={() => selectedId = dev.id}
            >
              <div class="device-info">
                <span class="icon">{iconMap[dev.type] || '💧'}</span>
                <span class="name">{dev.name}</span>
              </div>
              <div class="device-status">
                <span class="status-dot"></span>
              </div>
            </button>
          {/each}
        </div>
      </div>
    </div>

    <!-- svelte-ignore a11y_click_events_have_key_events -->
    <div class="col-right hover-active" on:click={() => currentPage = 'history'}>
      <div class="right-header">
        <h3 class="section-title">Live Activity ›</h3>
        <LiveGraph data={flowHistory} />
      </div>
      <div class="bottom-graph-container">
        <UtilityGraph />
      </div>
    </div>

  </main>

  {:else if currentPage === 'history'}
  <main class="history-grid fade-in">
    <div class="col-left">
      <div class="year-selector">
        <!-- svelte-ignore a11y_label_has_associated_control -->
        <label>Statement Period:</label>
        <select>
          <option>2025 (Current)</option>
          <option>2024</option>
          <option>2023</option>
        </select>
      </div>
      <MasterGraph />
      <UtilityGraph />
    </div>

    <div class="col-wide">
      <h2>Detailed Statements</h2>
      <div class="statement-card">
        <div class="s-row header">
          <span>Date</span><span>Utility</span><span>Usage</span><span>Cost</span>
        </div>
        <div class="s-row">
          <span>Dec 09</span><span>Master Shower</span><span>45.5L</span><span>$2.27</span>
        </div>
        <div class="s-row">
          <span>Dec 08</span><span>Sprinklers</span><span>180L</span><span>$9.00</span>
        </div>
        <div class="s-row">
          <span>Dec 07</span><span>Kitchen Sink</span><span>12L</span><span>$0.60</span>
        </div>
        <div class="s-row">
          <span>Dec 06</span><span>Dishwasher</span><span>30L</span><span>$1.50</span>
        </div>
        <div class="s-row">
          <span> Dec 05 </span><span> Tap </span> <span> 6.7L</span> <span>$0.67</span> 
        </div>
        </div>
      </div>
  </main>

  {:else if currentPage === 'donate'}
  <main class="donate-container fade-in">
    <h2>Impact Payment</h2>
    <p class="subtitle">We encourage accountability. If you exceed your water target, match the cost as a donation to conservation efforts.</p>

    <div class="donate-card">
      <div class="status-row">
        <span>Your Target:</span>
        <strong>{totalLimit} L</strong>
      </div>
      <div class="status-row">
        <span>Actual Usage:</span>
        <strong class:danger={isOverBudget}>{totalUsage.toFixed(2)} L</strong>
      </div>
      
      <div class="divider"></div>

      {#if isOverBudget}
        <div class="penalty-box">
          <div class="penalty-icon">⚠️</div>
          <div class="penalty-info">
            <h3>Limit Exceeded by {overageAmount.toFixed(2)} L</h3>
            <p>You have gone over your monthly water budget.</p>
          </div>
        </div>

        <div class="final-amount">
          <span>Suggested Donation Match (2x Penalty)</span>
          <div class="money">${(donationSuggestion * 2).toFixed(2)}</div>
        </div>

        <button class="donate-btn" on:click={() => window.open('https://water.org/donate/', '_blank')}>
          Pay & Donate to Water.org
        </button>
      {:else}
        <div class="success-box">
          <div class="success-icon">🎉</div>
          <div>
            <h3>Great Job, Aditya!</h3>
            <p>You are under your limit. No penalty payment required this month.</p>
          </div>
        </div>
        
        <button class="donate-btn secondary" on:click={() => window.open('https://water.org/donate/', '_blank')}>
          Make a Voluntary Donation
        </button>
      {/if}
    </div>
  </main>
  {/if}

  {#if showAddModal}
    <!-- svelte-ignore a11y_click_events_have_key_events -->
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div class="modal-backdrop" on:click|self={() => showAddModal = false}>
      <div class="modal">
        <h2>Add New Utility</h2>
        <form on:submit={handleAddDevice}>
          <div class="input-group">
            <!-- svelte-ignore a11y_label_has_associated_control -->
            <label>Name</label>
            <input type="text" name="name" placeholder="e.g. Guest Bathroom" required />
          </div>
          <div class="input-group">
            <!-- svelte-ignore a11y_label_has_associated_control -->
            <label>Type</label>
            <select name="type">
              <option value="tap">Tap / Faucet</option>
              <option value="shower">Shower</option>
              <option value="dishwasher">Dishwasher</option>
              <option value="toilet">Toilet</option>
              <option value="washer">Washing Machine</option>
              <option value="lawn">Sprinkler</option>
            </select>
          </div>
          <div class="input-group">
            <!-- svelte-ignore a11y_label_has_associated_control -->
            <label>Daily Limit (Liters)</label>
            <input type="number" name="limit" placeholder="100" required />
          </div>
          <div class="modal-actions">
            <button type="button" class="btn-cancel" on:click={() => showAddModal = false}>Cancel</button>
            <button type="submit" class="btn-save">Add Utility</button>
          </div>
        </form>
      </div>
    </div>
  {/if}

  {#if showLimitModal}
    <!-- svelte-ignore a11y_click_events_have_key_events -->
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div class="modal-backdrop" on:click|self={() => showLimitModal = false}>
      <div class="modal">
        <h2>Set Monthly Target</h2>
        <form on:submit={handleUpdateLimit}>
          <div class="input-group">
            <!-- svelte-ignore a11y_label_has_associated_control -->
            <label>Target Limit (Liters)</label>
            <input type="number" name="limit" value={globalLimit} required />
          </div>
          <div class="modal-actions">
            <button type="button" class="btn-cancel" on:click={() => showLimitModal = false}>Cancel</button>
            <button type="submit" class="btn-save">Update Target</button>
          </div>
        </form>
      </div>
    </div>
  {/if}

</div>

<style>
  .app-container { min-height: 100vh; background-color: var(--bg-body); padding-bottom: 2rem; }
  .fade-in { animation: fadeIn 0.3s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }

  /* --- DASHBOARD GRID --- */
  .dashboard-grid {
    display: grid; 
    grid-template-columns: 1fr 1.5fr 1fr; 
    gap: 2.0rem;
    max-width: 1500px; 
    margin: 0 auto; 
    padding: 0 1.5rem; 
    align-items: stretch; /* Forces all columns to be equal height */
  }

  /* Shared column styles for alignment */
  .col-left, .col-center, .col-right {
    display: flex;
    flex-direction: column;
    height: 100%; /* Important: makes the column fill the grid cell */
    gap: 1.5rem;
  }

  /* Left Column: Pushes cost card to bottom */
  .col-left {
    justify-content: space-between; 
  }
  .top-group {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }

  /* Center Column: Utility Manager fills space */
  .utility-manager { 
    background: var(--bg-card); 
    border: 1px solid var(--border); 
    border-radius: 12px; 
    padding: 1.5rem; 
    flex: 1; 
    display: flex;
    flex-direction: column;
  }
  

  .col-right { 
    border-radius: 12px; 
  }
  .bottom-graph-container {
    flex: 1; 
    display: flex;
    flex-direction: column;
  }

  .bottom-graph-container :global(> div) {
    height: 100%;
  }
  
  .hover-active:hover { background: rgba(255,255,255,0.03); cursor: pointer; }
  .section-title { font-size: 1.0rem; color: var(--text-muted); text-transform: uppercase; margin: 0 0 -0.5rem 0.5rem; }

  .manager-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem; }
  .manager-header h3 { margin: 0; font-size: 1.1rem; }
  .master-add-btn { background: var(--primary); color: rgb(2, 2, 2); border: none; padding: 0.5rem 1rem; border-radius: 6px; font-weight: 600; cursor: pointer; font-size: 0.9rem; }
  
  /* Make device list fill the now-taller utility manager */
  .device-list { 
    display: flex; 
    flex-direction: column; 
    gap: 0.5rem; 
    overflow-y: auto; 
    flex: 1; /* Fills the rest of the card */
  }
  
  .device-item { background: transparent; border: 1px solid var(--border); border-radius: 8px; padding: 0.8rem; display: flex; justify-content: space-between; align-items: center; cursor: pointer; color: var(--text-muted); transition: 0.2s; }
  .device-item:hover { background: rgba(255,255,255,0.03); color: var(--text-main); }
  .device-item.selected { border-color: var(--primary); background: rgba(59, 130, 246, 0.1); color: var(--text-main); }
  .device-info { display: flex; align-items: center; gap: 0.8rem; font-weight: 500; font-size: 1rem; }
  .status-dot { width: 8px; height: 8px; background: #444; border-radius: 50%; display: block; }
  .device-item.running .status-dot { background: #22c55e; box-shadow: 0 0 6px #22c55e; }


  .history-grid { display: grid; grid-template-columns: 1fr 2fr; gap: 2rem; max-width: 1200px; margin: 0 auto; padding: 0 1.5rem; }
  .year-selector { margin-bottom: 1rem; }
  .statement-card { background: var(--bg-card); border: 1px solid var(--border); border-radius: 12px; overflow: hidden; }
  .s-row { display: grid; grid-template-columns: 1fr 2fr 1fr 1fr; padding: 1rem; border-bottom: 1px solid var(--border); }
  .s-row.header { background: rgba(255,255,255,0.05); font-weight: bold; color: var(--text-muted); }

  .donate-container { max-width: 600px; margin: 0 auto; padding: 2rem; text-align: center; }
  .subtitle { color: var(--text-muted); margin-bottom: 2rem; }
  .donate-card { background: var(--bg-card); border: 1px solid var(--border); border-radius: 12px; padding: 2rem; }
  .status-row { display: flex; justify-content: space-between; margin-bottom: 1rem; font-size: 1.1rem; }
  .danger { color: #ef4444; }
  .divider { height: 1px; background: var(--border); margin: 1.5rem 0; }
  .penalty-box, .success-box { background: rgba(239, 68, 68, 0.1); padding: 1rem; border-radius: 8px; border: 1px solid #ef4444; display: flex; align-items: center; gap: 1rem; text-align: left; margin-bottom: 2rem; }
  .success-box { background: rgba(34, 197, 94, 0.1); border-color: #22c55e; }
  .penalty-icon, .success-icon { font-size: 2rem; }
  .penalty-info h3, .success-box h3 { margin: 0 0 0.25rem 0; font-size: 1rem; }
  .penalty-info p, .success-box p { margin: 0; font-size: 0.9rem; opacity: 0.9; }
  .final-amount { display: flex; flex-direction: column; gap: 0.5rem; margin-bottom: 2rem; }
  .money { font-size: 3rem; font-weight: 800; color: var(--text-main); }
  .donate-btn { background: var(--primary); color: rgb(0, 0, 0); width: 100%; padding: 1rem; border: none; border-radius: 8px; font-size: 1.1rem; font-weight: bold; cursor: pointer; transition: 0.2s; }
  .donate-btn:hover { background: var(--primary-hover); }
  .donate-btn.secondary { background: transparent; border: 1px solid var(--border); color: var(--text-muted); }
  .donate-btn.secondary:hover { border-color: var(--text-main); color: var(--text-main); }

  .modal-backdrop { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); display: flex; justify-content: center; align-items: center; z-index: 100; }
  .modal { background: var(--bg-card); padding: 2rem; border-radius: 12px; border: 1px solid var(--border); width: 320px; }
  .input-group { margin-bottom: 1rem; }
  label { display: block; margin-bottom: 0.5rem; color: var(--text-muted); font-size: 0.9rem; }
  input, select { width: 100%; padding: 0.6rem; border-radius: 6px; border: 1px solid var(--border); background: #111; color: white; box-sizing: border-box; }
  .modal-actions { display: flex; gap: 1rem; margin-top: 1.5rem; }
  .btn-save { background: var(--primary); color: rgb(0, 0, 0); border: none; padding: 0.6rem 1rem; border-radius: 6px; cursor: pointer; flex: 1; font-weight: bold; }
  .btn-cancel { background: transparent; color: var(--text-muted); border: 1px solid var(--border); padding: 0.6rem 1rem; border-radius: 6px; cursor: pointer; }
</style>