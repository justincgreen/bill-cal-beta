<script lang="ts">
  export let fromParent: any;
  export let calendarDays: Array<number>;
  
  let payDayOneNumber: number = 0;
    
  const handlePaydayForm = () => {
    let numberMatch = calendarDays.includes(payDayOneNumber);    
    // console.log(typeof payDayOneNumber)
    // console.log(numberMatch); 
    
    // Find matched number on calendar block and add a active class to block span 
    if(numberMatch) {
      document.querySelectorAll('.c-cal-block span').forEach((block) => {
        // console.log(block.classList[1]);
        if(block.classList[1] === `test-${payDayOneNumber}`) {
          block.classList.add('is-payday')
        }
      })
      
      // Close modal
      fromParent();
    }
  }
  
  // console.log(calendarDays)
</script>
<div class="c-modal__pay">
  <div class="c-modal__panel">
    <h3>Pay Date 1 <br> Type day of month number</h3>
    <input type="number" min="1" max="31" bind:value={payDayOneNumber}>
    <div>
      <button on:click|preventDefault={handlePaydayForm}>Submit</button>
    </div>    
  </div>
  <button on:click={fromParent}>Close Modal</button>
</div>

<style lang="scss">  
  .c-modal {  
    &__pay {
      display: grid;
      align-content: center;
      justify-content: center;
      background-color: rgba(0,0,0, 0.5);    
      position: fixed;
      inset: 0;
      transition: all 0.5s ease;
      z-index: 100;
    }
    
    &__panel {
      width: 400px;
      height: 300px;
      padding: 20px;
      text-align: center;
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