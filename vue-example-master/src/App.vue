<template>
  <div id='app'>
    <img alt='Vue logo' src='./assets/logo.png' />
    <hr>
    <h1 align="center"> To do list </h1><br>
    <!-- Create task form -->
    <div class="creatNewTask">
      <span>
        <input type='text' class="inputTask" v-model="newTask" />&nbsp;
        <button
          type="button"
          class="buttonAdd"
          v-on:click="onCreateNewTask"
        >
          Create new task
        </button>
      </span>
    </div>
    <br>
    <!-- Task table -->
    <div class="taskTable">
      <table>
        <tr v-for="task in tasks" v-bind:key="task.id" >
          <td>
            <input type="checkbox" v-model="task.done">
          </td>
          <td>
            <p :style="task.done && { textDecoration: 'line-through' }" >{{ task.name }}</p>
          </td>
          <td>
            <button
              type="button"
              class="buttonDelete"
              v-on:click="() => onDeleteTask(task.id)"
            >
              Delete
            </button>
          </td>
        </tr>
      </table>
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newTask: '',
      tasks: [],
    };
  },
  methods: {
    onCreateNewTask() {
      this.tasks = [
        {
          id: new Date().getTime(),
          name: this.newTask,
          done: false,
        },
        ...this.tasks,
      ];
      this.newTask = '';
    },
    onDeleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>

<style>
#app {
  text-align: center;
}

.creatNewTask {
  margin-bottom: 10px;
}
.creatNewTask .inputTask {
  /* border: #CCCCFF; */
  width: 30%;
  height: 28px;
}
.creatNewTask .buttonAdd {
  background-color: #CCCCFF;
  border: #CCCCFF;
  height: 35px;
  margin-left: 10px;
}

.buttonDelete {
  background-color: red;
  border: red;
  color: aliceblue;
}

.taskTable table {
  background-color: aliceblue;
  margin: 0px auto;
  width: 42%;
}

.taskTable p {
  text-align: left;
  margin-right: 0.87rem;
  margin-left: auto;
  display: inline-block;
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 16px;
  color: #4273DE;
}

</style>
