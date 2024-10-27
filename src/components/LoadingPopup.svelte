<script>
    import { fade, scale } from 'svelte/transition';
    export let isOpen = false; 
</script>

{#if isOpen}
<div class="overlay" transition:fade={{ duration: 500 }}>
  <div class="popup" transition:scale={{ duration: 500 }}>
    <div class="spinner"></div>
  </div>
</div>
{/if}


<style>
    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: #eee; 
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 1000;
    }
  
    .popup {
      /* background: white;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); */
      padding: 20px;
      border-radius: 8px;
      text-align: center;
      
      display: flex;
      flex-direction: column;
      align-items: center;
    }
  
    .spinner {
      border: 4px solid rgba(0, 0, 0, 0.1);
      border-top: 4px solid #163309;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
      margin-bottom: 10px;
    }
  
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
  </style>
  
