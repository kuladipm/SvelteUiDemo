<script>
    import SearchTodo from "./SearchTodo.svelte";
    import { createEventDispatcher } from "svelte";
    export  let todoItem;
    export let defaultDate;
 
  let dispatch = createEventDispatcher();
  function addItemInTodo() {
    dispatch("onEnter",{todoItem,defaultDate});
  }
</script>
  <div class="inputMain" style="width:100%">
    <span class="inputDive">
      <input
        type="text"
        class="input"
        on:keypress={(e) => {
          if (e.key === "Enter") {
            addItemInTodo();
          }
        }}
        bind:value={todoItem}
        placeholder="Add Your New Todo "
      />
    </span>
    <span class="dateDive">
      <input class="dateInput" type="date" bind:value={defaultDate} />
    </span>
  </div>
  