<script lang="ts">
  import { getContext } from 'svelte'
  const toastValue = getContext('toastContext');   
  const toastDisplay = getContext('toastToggle');   
</script>

{#if $toastDisplay}
  <div class="c-toast">
    { $toastValue }
  </div>
{/if}

<style lang="scss">
  .c-toast {
    display: inline-flex;
    border-radius: 5px;
    padding: 20px;
    background-color: lightgreen;
    
  }
</style>