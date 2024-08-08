<script lang="ts">
  import { getContext } from 'svelte'
  const toastValue = getContext('toastContext');   
</script>

<div class="c-toast">
  { $toastValue }
</div>