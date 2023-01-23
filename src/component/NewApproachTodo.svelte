<script>
  import "iconify-icon";
  import AddTodoEvent from "./AddTodoEvent.svelte";
  import { fade, fly } from "svelte/transition";
  export let status;
  export let buttonStatus = "todoAdd";
  export let todoItem;
  export let defaultDate;
  export let todoItemList;
  export let searchDate = "";
  // let defaultDate='';
  const addItemInTodo = () => {
    if (todoItem === "") {
      // alert(" please enter items in todo");
    } else {
      todoItemList = [
        ...todoItemList,
        {
          id: todoItemList.length + 1,
          Title: todoItem,
          status: status,
          date: defaultDate,
        },
      ];
      todoItem = "";
      //console.log(todoItemList);
      //sort array based on date
      todoItemList.sort(function (a, b) {
        let c = new Date(a.date);
        let d = new Date(b.date);
        return c - d;
      });
      defaultDate;
    }
  };
  const deleteItem = (i) => {
    todoItemList.splice(i, 1);
    todoItemList = todoItemList;
  };

  const showArray = todoItemList.sort(function (a, b) {
    var c = new Date(a.date);
    var d = new Date(b.date);
    return c - d;
  });
  //console.log(showArray);

  const buttonStatusOnEvent = (event) => {
    if (event.detail.buttonStatus === "showClicked") {
      buttonStatus = "showClicked";
    } else if (event.detail.buttonStatus === "inCompleteClicked") {
      buttonStatus = "inCompleteClicked";
    } else buttonStatus = "activeClicked";
  };
</script>

<!-- markup -->
<div class="sub-container">
  <h5>
    TODO LIST
    <iconify-icon
      icon="material-symbols:patient-list"
      style="color: black;"
      width="25"
      height="25"
    />
  </h5>
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
        placeholder="Add Todo "
      />
    </span>
    <span class="dateDive">
      <input class="dateInput" type="date" bind:value={defaultDate} />
    </span>
  </div>
  <!-- showing added item -->
  <!-- {#if buttonStatus === 3} -->
</div>

<div class="outPut-container">
  <div>
    {#each todoItemList as item, i}
      {#if buttonStatus === "todoAdd" || buttonStatus === "showClicked"}
        <div class="card" in:fade={{ y: 200, duration: 500 }} out:fade>
          <div class="card-body">
            <div class="row">
              <div class:checked={item.status} class="column">
                <input
                  type="checkbox"
                  class="checkBox"
                  bind:checked={item.status}
                />
              </div>
              <div class:checked={item.status} class="columnInput1">
                {item.Title}
              </div>
              <div class="columnInput2">
                {item.date}
              </div>
              <!-- svelte-ignore a11y-click-events-have-key-events -->
              <div
                class="columnDelete"
                on:click={() => {
                  deleteItem(i);
                }}
              >
                <iconify-icon
                  icon="material-symbols:delete"
                  style="color: red;"
                  width="18"
                  height="18"
                />
              </div>
            </div>
          </div>
        </div>
      {:else if buttonStatus === "activeClicked" && item.status === true}
        <div class="card" in:fade={{ y: 200, duration: 100 }} out:fade>
          <div class="card-body">
            <div class="row">
              <div class:checked={item.status} class="column">
                <input
                  type="checkbox"
                  class="checkBox"
                  bind:checked={item.status}
                />
              </div>
              <div class:checked={item.status} class="columnInput1">
                {item.Title}
              </div>
              <div class="columnInput2">
                {item.date}
              </div>
              <!-- svelte-ignore a11y-click-events-have-key-events -->
              <div
                class="columnDelete"
                on:click={() => {
                  deleteItem(i);
                }}
              >
                <iconify-icon
                  icon="material-symbols:delete"
                  style="color: red;"
                  width="18"
                  height="18"
                />
              </div>
            </div>
          </div>
        </div>
      {:else if buttonStatus === "inCompleteClicked" && item.status === false}
        <div class="card">
          <div class="card-body">
            <div class="row">
              <div class:checked={item.status} class="column">
                <input
                  type="checkbox"
                  class="checkBox"
                  bind:checked={item.status}
                />
              </div>
              <div class:checked={item.status} class="columnInput1">
                {item.Title}
              </div>
              <div class="columnInput2">
                {item.date}
              </div>
              <!-- svelte-ignore a11y-click-events-have-key-events -->
              <div
                class="columnDelete"
                on:click={() => {
                  deleteItem(i);
                }}
              >
                <iconify-icon
                  icon="material-symbols:delete"
                  style="color: red;"
                  width="18"
                  height="18"
                />
              </div>
            </div>
          </div>
        </div>
      {:else if buttonStatus === "searchDateEntered" && item.date === searchDate}
        <div class="card" in:fade={{ x: -200, duration: 500 }} out:fade>
          <div class="card-body">
            <div class="row">
              <div class:checked={item.status} class="column">
                <input
                  type="checkbox"
                  class="checkBox"
                  bind:checked={item.status}
                />
              </div>
              <div class:checked={item.status} class="columnInput1">
                {item.Title}
              </div>
              <div class="columnInput2">
                {item.date}
              </div>
              <!-- svelte-ignore a11y-click-events-have-key-events -->
              <div
                class="columnDelete"
                on:click={() => {
                  deleteItem(i);
                }}
              >
                <iconify-icon
                  icon="material-symbols:delete"
                  style="color: red;"
                  width="18"
                  height="18"
                />
              </div>
            </div>
          </div>
        </div>
      {/if}
    {/each}
    {#if todoItemList.length !== 0}
      <div class="sub-container1">
        <AddTodoEvent on:message={buttonStatusOnEvent} />
        <input
          class="searchData"
          onfocus="(this.type='date')"
          placeholder="Search Todo"
          on:change={() => {
            buttonStatus = "searchDateEntered";
          }}
          bind:value={searchDate}
        />
      </div>
    {/if}
  </div>
</div>

<!-- css -->
<style>
  .column {
    float: left;
    width: 4.33%;
  }
  .columnInput1 {
    float: left;
    width: 45.33%;
    margin-right: 1%;
  }

  .columnInput2 {
    float: left;
    width: 35.33%;
  }
  .columnDelete {
    width: 1.33%;
  }
</style>
