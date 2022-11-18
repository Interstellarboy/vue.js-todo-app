<template>
  <div class="flex justify-center m-20 text-white">
    <span class="text-3xl text-white">Task Tracker</span>
    <button class="button-21" @click="this.flag = !this.flag">Add Todos</button>
  </div>
  <div class="m-10">
    <form @submit="addNewTask" v-show="flag" class="">
      <input
        class="p-2 rounded-xl text-black w-full content-center"
        v-model="text"
        placeholder="add task here"
      />
      <div class="flex">
        <h1 class="text-sm">Set Reminder?</h1>
        <input v-model="check" type="checkbox" />
      </div>
      <button class="button-21 mb-10">submit</button>
    </form>

    <div class="flex-col justify-center items-center">
      <div
        v-for="(item, index) in array"
        :key="index"
        @dblclick="togglecompleted(item.id)"
        :class="{ active: !item.completed }"
        class="flex justify-between bg-neutral-600 rounded-xl"
      >
        <span class="inline p-5=3 m-3">{{ item.text }}</span>
        <img
          @click="deleteTask(item.id)"
          class="delete inline"
          src="../assets/delete.gif"
          alt="delete"
        />
      </div>
    </div>
    <div class="flex justify-center">
      <button class="button-21 mt-10 btn" @click="clearCompleted">
        Clear Completed
      </button>
    </div>
  </div>
  <div @texts="childToParent"></div>
</template>

<script>
import Task from "./Task.vue";
export default {
  components: {
    Task,
  },
  data() {
    return {
      idd: 2,
      name: "alpit",
      surname: "sonawane",
      array: [
        { id: 1, text: "This is first todo", completed: false },
        { id: 2, text: "This is second todo", completed: false },
      ],
      text: "",
      flag: false,
      check: false,
    };
  },
  methods: {
    childToParent(txt) {
      console.log(txt);
    },

    addNewTask(e) {
      e.preventDefault();
      if (this.text == null) return (this.text = "enter valid tasks");
      this.array.push({
        id: this.idd + 1,
        text: this.text,
        completed: !this.check,
      });
      this.idd = this.idd + 1;
      this.text = "";
    },
    togglecompleted(id) {
      const map = this.array.filter((item) => item.id == id);
      map[0].completed = !map[0].completed;
    },
    deleteTask(id) {
      const map = this.array.filter((item) => item.id !== id);
      this.array = map;
    },
    clearCompleted() {
      const map = this.array.filter((item) => item.completed == false);
      this.array = map;
    },
  },
};
</script>

<style scoped>
* {
  margin: 5px;
}

.button-21 {
  align-items: center;
  background: #f5f5fa;
  border: 0;
  border-radius: 8px;
  box-shadow: -5px -5px 10px 0 #fff, 5px 5px 10px 0 #1d0dca17;
  box-sizing: border-box;
  color: #2a1f62;
  cursor: pointer;
  display: flex;
  font-family: "Cascadia Code", Consolas, Monaco, "Andale Mono", "Ubuntu Mono",
    monospace;
  font-size: 1rem;
  justify-content: center;
  line-height: 1.5rem;
  padding: 15px;
  position: relative;
  text-align: left;
  transition: 0.2s;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  white-space: pre;
  width: max-content;
  word-break: normal;
  word-spacing: normal;
}

.button-67:hover {
  background: #f8f8ff;
  box-shadow: -15px -15px 30px 0 #fff, 15px 15px 30px 0 #1d0dca17;
}

@media (min-width: 768px) {
  .button-67 {
    padding: 24px;
  }
}

/* Parent background */
#F5F5FA.button-21 {
  width: 200px;
  align-items: center;
  appearance: none;
  background-color: #3eb2fd;
  background-image: linear-gradient(1deg, #4f58fd, #149bf3 99%);
  background-size: calc(100% + 20px) calc(100% + 20px);
  border-radius: 100px;
  border-width: 0;
  box-shadow: none;
  box-sizing: border-box;
  color: #ffffff;
  cursor: pointer;
  display: inline-flex;
  font-family: CircularStd, sans-serif;
  font-size: 1rem;
  height: auto;
  justify-content: center;
  line-height: 1.5;
  padding: 6px 20px;
  position: relative;
  text-align: center;
  text-decoration: none;
  transition: background-color 0.2s, background-position 0.2s;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: top;
  white-space: nowrap;
}

.button-21:active,
.button-21:focus {
  outline: none;
}

.button-21:hover {
  background-position: -20px -20px;
}

.button-21:focus:not(:active) {
  box-shadow: rgba(40, 170, 255, 0.25) 0 0 0 0.125em;
}

.active {
  border-left: 5px solid green;
}
.delete {
  height: 20px;
  width: 20px;
  padding: 1px;
  border-radius: 50%;
}
span {
  text-align: center;
}
</style>
