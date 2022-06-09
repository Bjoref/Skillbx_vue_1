<template>
  <h1>Список задач</h1>
  <div v-if="count() <= 0">0</div>
  <div v-else-if="count() <= 1">1</div>
  <div v-else>Осталось сделать задач: <span class="counter">{{ count() }}</span></div>
  <div class="list">
    <div class="item" :class="{done: task.done}" v-for="(task, index) in tasks" :key='index'>
      <input type="checkbox" v-model="task.done">
      {{ task.itemText }}
    </div>
  </div>
  <div class="form">
    <input :placeholder="message" v-model="message" @keyup.enter='addTask'>
    <button type="button" @click="addTask">Добавить</button>
  </div>
  <transition :name="this.animationClass">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/American_Beaver.jpg/275px-American_Beaver.jpg" v-show="count() <= 0">
  </transition>
</template>

<script>
export default {
  name: 'ToDoList',
  data() {
    return {
    animationClass: 'bounce',
    disabled: 'disabled',
    button: 'submit',
    tasks: [
      {itemText: 'dsfdsf', done: false},
      {itemText: 'fsdfsd', done: false},
      {itemText: '3', done: true},
    ]
    }
  },
  methods: {
    addTask(){
        this.tasks.push({itemText: this.message, done: false}); 
        this.message='';
    },
    count(){
      return this.tasks.filter(task => !task.done).length;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list {
  padding: 20px;
  border: 1px solid #ccc;
  margin: 20px 0;
}
.item {
  margin: 10px 0;
}
.done {
  text-decoration: line-through;
}
.form {
  margin: 20px 0;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
.bounce-enter-active {
  animation: 1s linear 0s normal none infinite running rotate;
}
.bounce-leave-active {
  animation: bounce-in .5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
