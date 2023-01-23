<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
</script>

<button on:click={() => dispatch("message", { buttonStatus: "showClicked" })} class="displayAllBtn"
  >Show All</button
>
<button on:click={() => dispatch("message", { buttonStatus: "activeClicked" })} class="completeBtn"
  >Complete</button
>
<button on:click={() => dispatch("message", { buttonStatus: "inCompleteClicked" })} class="activeBtn"
  >active</button
>
