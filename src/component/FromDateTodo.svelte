<script>
    import "iconify-icon";
    let status = false;
    let count = 0;
    let todoItem = "";
    let todoItemList = [];
    // let defaultDate='';
    const date = new Date();
    let day = date.getDate();
    let month = String(date.getMonth() + 1).padStart(2, "0");
    let year = date.getFullYear();
    $: defaultDate = year + "-" + month + "-" + day;
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
      }
    };
    let searchFromDate;
    let searchToDate;
  
  
    const activeItem = () => {
      count = 1;
    };
    const completeItem = () => {
      count = 2;
    };
    const allTodo = () => {
      count = 4;
    };
    const deleteItem = (i) => {
      todoItemList.splice(i, 1);
      todoItemList = todoItemList;
    };
  function getDatesInRange(startDate, endDate) {
    const date = new Date(startDate.getTime());
  
    const dates = [];
  
    while (date <= endDate) {
      dates.push(new Date(date));
      date.setDate(date.getDate() + 1);
    }
  
    return dates;
  }
  
  const d1 = new Date(searchFromDate);
  const d2 = new Date(searchToDate);
  
  console.log(getDatesInRange(d1, d2));
    const showArray = todoItemList.sort(function (a, b) {
      var c = new Date(a.date);
      var d = new Date(b.date);
      return c - d;
    });
    //console.log(showArray);
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
          placeholder="Add Your New Todo "
        />
      </span>
      <span class="dateDive">
        <input class="dateInput" type="date" bind:value={defaultDate} />
      </span>
    </div>
    <div class="sub-container1">
      <label for="input">Search:</label><span>From</span>
      <input
        type="date"
        class=""
        on:change={
          ()=>{count=5}
            
        }
        bind:value={searchFromDate}
      />
      <label for="">To</label>
      <input
        type="date"
        class=""
        on:change={
          ()=>{count=6}
            
        }
        bind:value={searchToDate}
      />
    </div>
    <div class="sub-container1">
      <button on:click={allTodo} class="displayAllBtn">Show All</button>
      <button on:click={completeItem} class="completeBtn">Complete</button>
      <button on:click={activeItem} class="activeBtn">active</button>
    </div>
  
    <!-- showing added item -->
    <!-- {#if count === 3} -->
    {#each todoItemList as item, i}
      {#if count === 0 || count === 4}
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
      {:else if count === 2 && item.status === true}
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
      {:else if count === 1 && item.status === false}
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
      {:else if count === 5 && (item.date >=searchFromDate && item.date<=searchToDate)}
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
      {/if}
    {/each}
  </div>
  
  <!-- css -->
  <style>
    .checked {
      text-decoration: line-through;
      opacity: 20%;
    }
    .sub-container {
      background-color: rgb(231, 221, 218);
      margin: 5% 32%;
      border-radius: 6px;
      border: 1px solid black;
      color: black;
      text-align: center;
      padding: 5px;
    }
    .searchData {
      margin: 1%;
      padding: 1%;
      border: 0.5px solid black;
      border-radius: 5px;
      text-align: center;
      border-radius: 5px;
      width: 40%;
    }
    #searchBtn {
      margin: 1px;
      padding: 1%;
      border: 0.5px solid black;
      border-radius: 5px;
      text-align: center;
      border-radius: 5px;
      width: 16%;
      background-color: ivory;
    }
    .inputDiv {
      width: 60%;
      border-radius: 15px;
    }
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
    .columnDelete:hover,
    .checkBox:hover,
    .dateInput {
      cursor: pointer;
    }
    h5 {
      color: brown;
      width: 60%;
      margin: 2% 21%;
      padding: 1px;
      text-align: center;
    }
    h6 {
      display: block;
      color: black;
      width: fit-content;
      margin: 0% 32%;
      padding: 10px;
    }
    .input {
      margin: 1px;
      padding: 1%;
      border: 0.5px solid black;
      border-radius: 5px;
      text-align: center;
      border-radius: 5px;
      width: 60%;
    }
    .dateInput {
      margin: 1px;
      padding: 1%;
      border: 0.5px solid black;
      border-radius: 5px;
      text-align: left;
      border-radius: 5px;
      width: 26%;
      background-color: ivory;
    }
    /* .addItemButton {
          border-radius: 10px;
          border-color: rgb(15, 7, 7);
          background-color:white;
          width: 5% 5%;
          padding: 5px;
          font-size: small;
          margin: 1%;
          text-align: center;
        } */
    .completeBtn,
    .activeBtn,
    .displayAllBtn {
      border-radius: 3px;
      border: 1.3px solid black;
      background-color: rgb(223, 223, 232);
      width: 17.5%;
      padding: 5px;
      font-size: 80%;
      margin: 5% 1%;
    }
    .completeBtn:hover,
    .activeBtn:hover,
    .displayAllBtn:hover {
      background-color: rgb(201, 201, 238);
    }
    .card {
      margin: 0% 12%;
      font-size: 15px;
      border-radius: 6px;
      border: 0.2px solid black;
      text-align: left;
      display: flexbox;
      flex-wrap: initial;
    }
  </style>
  