<script lang="ts">
  
</script>

<div class="c-modal">
  <div class="c-modal__panel">
    <h2>Modal Panel Header</h2>
    <button>Mark Pay Day</button>
    <button>Add Bill</button>
    <button>Close</button>
  </div>
</div>

<style lang="scss">
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
  }
</style>