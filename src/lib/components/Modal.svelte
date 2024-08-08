<script lang="ts">
  import { getContext } from 'svelte'
  const toastValue = getContext('toastContext');
  
 export let modalData: any; 
 export let panelBlockInfo: any; 
 
 // Handlers
 const closeModal = () => {
  modalData.show = false;
 }
 
 const handlePayDay = (e: any) => {
  let blockElement = document.querySelector(`.${panelBlockInfo.blockClass}`);  
  blockElement ? blockElement.classList.toggle('is-payday') : null;
  
  // Control button text from within modal panel  
  if(panelBlockInfo.buttonText === 'Mark Pay Day') {
    panelBlockInfo.buttonText = 'Remove Pay Day';
    toastValue.set('Payday marked');    
  }else {
    panelBlockInfo.buttonText = 'Mark Pay Day';
    toastValue.set('Payday removed'); 
  }
 }
</script>

{#if modalData.show}
<div class="c-modal is-active" on:click|self={closeModal}>
  <div class="c-modal__panel">
    <h2>Modal Panel Header</h2>
    <button on:click={handlePayDay}>{ panelBlockInfo?.buttonText }</button>
    <button>Add Bill</button>
    <button on:click={closeModal}>Close</button>
    
    <div class="c-modal__panel-date">Panel Date: { panelBlockInfo?.date }</div>
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