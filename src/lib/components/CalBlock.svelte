<script lang="ts">
  export let dateNumber: number;  
</script>

<div class="c-cal-block" on:click role="button"tabindex="0">
  <span class={`c-cal-block__date test-${dateNumber}`}>{ dateNumber }</span>
</div>

<style lang="scss">
  .c-cal-block {
    flex: 1 0 14.2857%;
    min-height: 40px;
    border-bottom: 1px solid black;
    border-left: 1px solid black;
    padding: 20px;
    cursor: pointer;
    
    &:last-of-type {
      border-right: 1px solid black;
    }                
  }    
  
  :global(.current-day > span) {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    padding: 5px;
    background: green;
    color: white;
    border-radius: 50%;
  }
  
  :global(.is-payday ) {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    padding: 5px;
    background: orangered;
    color: white;
  }
</style>