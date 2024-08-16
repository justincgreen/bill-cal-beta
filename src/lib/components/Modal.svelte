<script lang="ts">
  import { getContext } from 'svelte'
  import BillForm from '$lib/components/BillForm.svelte'
  const toastValue = getContext('toastContext');
  const toastDisplay = getContext('toastToggle');
  let billFormDisplay: boolean = false;
  
  export let modalData: any; 
  export let panelBlockInfo: any; 
 
 // Handlers
 const closeModal = () => {
  modalData.show = false;
  billFormDisplay = false;
 }
 
 const handlePayDay = (e: any) => {
  let blockElement = document.querySelector(`.${panelBlockInfo.blockClass}`);  
  blockElement ? blockElement.classList.toggle('is-payday') : null;
  
  // Control button text from within modal panel  
  if(panelBlockInfo.buttonText === 'Mark Pay Day') {
    panelBlockInfo.buttonText = 'Remove Pay Day';
    toastDisplay.set(true);
    toastValue.set('Payday marked');
    
    setTimeout(() => {
      toastDisplay.set(false);
    }, 1000)
  }else {
    panelBlockInfo.buttonText = 'Mark Pay Day';
    toastDisplay.set(true);    
    toastValue.set('Payday removed'); 
    
    setTimeout(() => {
      toastDisplay.set(false);
    }, 1000);

  }
 }
 
 const handleAddBill = () => {
    billFormDisplay = true;
 }
 
 const handleRemoveBillForm = () => {
     billFormDisplay = false;
  }
 
 // Format the date based on this expression -> panelBlockInfo?.date
 const handleFormatDate = (blockDate: string) => {
  const stringToNumber = parseInt(blockDate, 10);
  
  if(stringToNumber  === 1 || stringToNumber  === 21 || stringToNumber  == 31) {
    return stringToNumber + 'st'
  }else if(stringToNumber === 2 || stringToNumber === 22) {
    return stringToNumber + 'nd'
  }else if(stringToNumber === 3 || stringToNumber === 23) {
    return stringToNumber + 'rd'
  }else {
    return stringToNumber + 'th'
  }
 }
 
 // handleFormatDate(20);
</script>

{#if modalData.show}
<div class="c-modal is-active" on:click|self={closeModal}>
  <div class="c-modal__panel">
    <h2 class="c-modal__panel-date">{panelBlockInfo?.dayName} {panelBlockInfo?.currentMonth} { handleFormatDate(panelBlockInfo?.date) }, { panelBlockInfo?.currentYear }</h2>
    <button on:click={handlePayDay}>{ panelBlockInfo?.buttonText }</button>    
    {#if billFormDisplay}
      <button on:click={handleRemoveBillForm}>Remove Bill</button>
      {:else}
      <button on:click={handleAddBill}>Add Bill</button>
    {/if}
    <button on:click={closeModal}>Close</button>      
    
    {#if billFormDisplay}
      <BillForm />  
    {/if}
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