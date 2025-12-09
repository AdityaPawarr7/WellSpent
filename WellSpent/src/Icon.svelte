<script>
  export let name = "tap";
  export let size = "20";
  export let color = "currentColor";

  const icons = {
    // Water Tap / Faucet
    tap: "M4 19h16v2H4v-2zm7-2V6h2v11h-2zm-2 0V9h6v8H9zm2-14V1h2v2h-2zm-3 5V5h8v3h-8z",
    
    // Shower Head
    shower: "M12 22c4.97 0 9-4.03 9-9h-2c0 3.87-3.13 7-7 7s-7-3.13-7-7H3c0 4.97 4.03 9 9 9zM12 2C8.69 2 6 4.69 6 8h2c0-2.21 1.79-4 4-4s4 1.79 4 4h2c0-3.31-2.69-6-6-6zm-4 15h8v-2H8v2z",
    
    // Dishwasher (Square with racks)
    dishwasher: "M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 14H4V6h16v12zM6 8h12v2H6V8zm0 4h12v2H6v-2z",
    
    // Lawn Tap / Sprinkler
    lawn: "M12 2L8 6h3v5H5V8H3v8h2v-3h6v3h2v-3h6v3h2V8h-2v3h-6V6h3L12 2z",
    
    // Stats / Graph Icon
    graph: "M5 9.2h3V19H5zM10.6 5h2.8v14h-2.8zm5.6 8H19v6h-2.8z",

    // Edit / Pencil
    edit: "M3 17.25V21h3.75L17.81 9.94l-3.75-3.75L3 17.25zM20.71 7.04c.39-.39.39-1.02 0-1.41l-2.34-2.34c-.39-.39-1.02-.39-1.41 0l-1.83 1.83 3.75 3.75 1.83-1.83z"
  };
</script>

<svg 
  xmlns="http://www.w3.org/2000/svg" 
  width={size} 
  height={size} 
  viewBox="0 0 24 24" 
  fill={color}
  style="display: block;"
>
  <path d={icons[name] || icons.tap} />
</svg>