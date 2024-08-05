<script lang="ts">
  import { getContext } from 'svelte'
  const billsData = getContext('myContext');
</script>
{#if $billsData.length}
  <ul>
  {#each $billsData as bill (bill.billID)}
    <li>
      <p>Bill Name: {bill.billName}</p>
      <p>Bill Amount: {bill.billAmount}</p>
      <p>Bill Date: {bill.billDate}</p>
    </li>
  {/each}
  </ul>
  {:else}
  No bills to display
{/if}