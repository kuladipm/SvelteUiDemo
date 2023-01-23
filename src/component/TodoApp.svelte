<script>
   import NewApproachTodo from "./NewApproachTodo.svelte";
    const allVariableObject = {
      status: false,
      searchDate: "",
      todoItem: "",
      todoItemList: [],
    };
 
    const date = new Date();
    let day = date.getDate();
    let month = String(date.getMonth() + 1).padStart(2, "0");
    let year = date.getFullYear();
    $: defaultDate = year + "-" + month + "-" + day;
  </script>
  
  <NewApproachTodo {...allVariableObject}{defaultDate} />