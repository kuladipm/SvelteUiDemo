   <script>
  import { createEventDispatcher } from "svelte";
    let dispatch = createEventDispatcher();
  let buttonStatus="todoAdd";
let searchDate
   </script>
   <label for="input" style="color:cornflowerblue">SEARCH:</label>
    <input
      class="searchData"
      onfocus="(this.type='date')"
      placeholder="Search Todo"
      on:change={
        ()=>dispatch("change", { searchDate })
      }
      bind:value={searchDate}
    />