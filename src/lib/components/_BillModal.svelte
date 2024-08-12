<script lang="ts">
  export let fromBillParent: any; 
  let billName: string = '';
  let billAmount: string = '';
  let billDate: string = '';
  
  import { getContext } from 'svelte'
  const billsData = getContext('myContext');
  
  function generateRandomId(length = 8) {
    return Math.random().toString(36).substr(2, length);
  }
</script>

<div class="c-modal__bill">
  <div class="c-modal__panel">
    <h3>Bill Details</h3>
    <input type="text" placeholder="enter bill name" on:change={(e) => billName = e.currentTarget.value}>
    <input type="text" placeholder="enter bill amount" on:change={(e) => billAmount = e.currentTarget.value}>
    <input type="date" on:change={(e) => billDate = e.currentTarget.value}>
    <button on:click={
      () => {
        let newBill = {
          billID: generateRandomId(),
          billName,
          billAmount,
          billDate
        }
        $billsData = [...$billsData, newBill];
        // console.log($billsData)
      }}
      >      
      Add Bill Details
    </button>        
  </div>
  
  <button on:click={fromBillParent}>Close Modal</button>
</div>

<style lang="scss">
  .c-modal {  
    &__bill {
      display: grid;
      align-content: center;
      justify-content: center;
      background-color: rgba(0,0,0, 0.5);    
      position: fixed;
      inset: 0;
      transition: all 0.5s ease;
      z-index: 100;
      
      &.is-active {
        opacity: 1;
        visibility: visible;
        
        .c-modal__panel {
          transform: scale(1);
          opacity: 1;
        }
      }
    }
    
    &__panel {
      width: 400px;
      height: 300px;
      padding: 20px;
      background-color: #ffffff;
      color: #1A202C;
      border-radius: 5px;
      transition: all 0.3s ease;
      
      p {
        margin: 5px 0;
      }
    }
  }  
</style>