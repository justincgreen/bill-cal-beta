<script lang="ts">
  const handleBill = () => {
    alert();
  }
</script>

<div class="c-bill-form">
  <h3>Bill Form</h3>
  <div class="c-bill-form__wrapper">
    <input type="date">    
    <input type="text" placeholder="Bill Title">
    <input type="text" placeholder="Bill Amount">  
    <button on:click={handleBill}>Create Bill</button>
  </div>
</div>

<style lang="scss">
  .c-bill-form {
    background-color: coral;
    padding: 5px;  
    
    .c-bill-form__wrapper {
      padding: 10px;
      
      input {
        display: block;
        width: 100%;        
        padding: 10px;
        margin-bottom: 20px;
        border-radius: 5px;
        border: none;
        box-sizing: border-box;
      }            
    }  
    
    button {
      padding: 10px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  }
</style>