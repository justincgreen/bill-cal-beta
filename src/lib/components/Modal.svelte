<script lang="ts">
 export let modalData: any; 
 export let panelInfo: any; 
 
 // Handlers
 const closeModal = () => {
  modalData.show = false;
 }
 
 const handlePayDay = (e: any) => {
  alert('Payday');  
 }
</script>

{#if modalData.show}
<div class="c-modal is-active">
  <div class="c-modal__panel">
    <h2>Modal Panel Header</h2>
    <button on:click={handlePayDay}>Mark Pay Day</button>
    <button>Add Bill</button>
    <button on:click={closeModal}>Close</button>
    
    <div class="c-modal__panel-date">Panel Date: { panelInfo?.date }</div>
  </div>
</div>
{/if}

<style lang="scss">
  // Not being used currently
  :global(.is-active) { 
    display: grid !important;
  }
  .c-modal {
    display: none;
    align-content: center;
    justify-content: center;
    background-color: rgba(0,0,0, 0.3);
    position: fixed;
    inset: 0;      
    
    &__panel {
      width: 400px;
      min-height: 400px;
      padding: 20px;
      border-radius: 5px;
      background-color: #fff;
    }
    
    &__panel-date {
      padding: 20px 20px 20px 0;
    }
  }
</style>