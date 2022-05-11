<template>
  <div class="container">
    <!--TodoList-->
    <section id="TodoList">
      <header>
        <h1>
          ToDo List
          <span class="list__amount">{{ this.filterList.length }}</span>
        </h1>
        <div class="input__nav">
          <input @keydown.enter="addBtn" v-model="input" type="text" />
          <span @click="addBtn" class="addBtn">Add Task</span>
        </div>
      </header>

      <main>
        <ul class="todo__items">
          <li
            v-for="item in filterList"
            :key="item.id"
            class="animate__animated animate__fadeInDown"
          >
            <div class="todo__content">
              <input
                @click="
                  playSound(
                    'http://soundbible.com/mp3/Elevator Ding-SoundBible.com-685385892.mp3'
                  )
                "
                class="checkbox"
                id="checkbox"
                type="checkbox"
                @change="completeTask(item)"
                v-bind:checked="item.isComplete"
              />

              <span>{{ item.TodoText }}</span>
            </div>

            <button @click="removeTodoItems(item.id)" class="removeBtn">
              REMOVE
            </button>
          </li>
        </ul>
      </main>
    </section>

    <!--DoneList-->
    <section id="DoneList">
      <header>
        <h1>
          Done List
          <span class="list__amount">{{ this.filterList2.length }}</span>
        </h1>
      </header>

      <main>
        <ul class="done__items">
          <li
            v-for="(itemdone) in filterList2"
            :key="itemdone.id"
            class="animate__animated animate__slideInUp"
          >
            <div class="todo__content">
              <input
                @click="
                  playSound(
                    'http://soundbible.com/mp3/Air Plane Ding-SoundBible.com-496729130.mp3'
                  )
                "
                class="checkbox"
                id="checkbox"
                type="checkbox"
                v-model="itemdone.isComplete"
              />
              <span>{{ itemdone.TodoText }}</span>
            </div>

            <button @click="removeDoneItems(itemdone.id)" class="removeBtn">
              REMOVE
            </button>
          </li>
        </ul>
      </main>
    </section>
  </div>
</template>





<script>
export default {
  data() {
    return {
      TodoList: [],
      input: "",
      Error: false,
    };
  },

  methods: {
    addBtn() {
      if (!this.input) {
        this.Error = true;
        return;
      }

      this.TodoList.push({
        id: (new Date()).getTime(),
        TodoText: this.input,
        isComplete: false,
      }),
        (this.input = "");
    },

    removeTodoItems(id) {
      let index=this.TodoList.findIndex(item=>item.id==id);
      this.TodoList.splice(index, 1);
    },

    completeTask(TodoList) {
      TodoList.isComplete = !TodoList.isComplete;
    },

    playSound(sound) {
      if (sound) {
        var audio = new Audio(sound);
        audio.play();
      }
    },

    removeDoneItems(id) {
      let index=this.TodoList.findIndex(item=>item.id==id);
      this.TodoList.splice(index, 1);
    },
  },

  computed: {
    filterList: function () {
      return this.TodoList.filter((itemList) => itemList.isComplete == false);
    },
    filterList2: function () {
      return this.TodoList.filter((itemList) => itemList.isComplete == true);
    },
  },
};
</script>







<style scoped>
</style>