<script lang="ts">
  export let someParentData: any;
  
 // import { getContext } from 'svelte'
 // 
 // const customValue = getContext('myContext');
 // customValue.set('Updated Taco');
 // console.log(customValue)
</script>

<div class="c-panel">
  <button on:click={(e) => e.currentTarget.parentElement.classList.remove('is-active')}>Close Panel</button>
  <div>The block date is {someParentData}</div>
  <!-- <div>{$customValue}</div> -->
</div>

<style lang="scss">
  .c-panel {
    background: lightgrey;
    width: 50%;
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;   
    transform: translateX(100%);
    transition: all 0.2s ease; 
    
    /* &.is-active {
      transform: translateX(0%);
    } */
  }
  
  :global(.c-panel.is-active ) {
    transform: translateX(0%);
  }
</style>