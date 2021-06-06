<template>
  <div class="list">
    <h1>Lista de tarefas</h1>
    <div class="form">
      <form @submit.prevent="save()">
        <div class="input-data">
        <input type="text" placeholder="Escreva uma tarefa..." v-model="toDo" ref="taskInput">
        <button type="submit">Enviar</button>
        </div>
      </form>
      <p class="error-message" v-show="errorMessage">{{errorMessage}}</p>
    </div>
    <div class="to-do-list">
      <ol>
        <li v-for="task in toDoList" :key="task.text">
          <span class="text" :class="{'completed' : task.completed}">{{task.text}}</span>
          <span class="actions">
            <button class="complete" v-if="!task.completed" @click="complete(task)"><IconifyIcon :icon="icons.leftCheckMark" :style="{fontSize: '18px'}" /></button>
            <button class="remove" @click="remove(task)">&#10006;</button>
          </span>
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
import IconifyIcon from '@iconify/vue';
import leftCheckMark from '@iconify/icons-emojione-v1/left-check-mark';

export default {
  components: {
		IconifyIcon,
	},
  data(){
    return {
      icons: {
				leftCheckMark,
			},
      errorMessage: null,
      toDoList: [],
      toDo: ''
    }
  },
  methods: {
    save(){
      this.errorMessage = null
      if(!this.toDo){
        this.errorMessage = 'Digite o texto da tarefa!'
        return
      }
      this.toDoList.push({text: this.toDo, completed: false})
      this.toDo = ''
    },
    complete(task){
      task.completed = true
      // this.$set(task, 'completed', true)
    },
    remove(task){
      const index = this.toDoList.indexOf(task)
      this.toDoList.splice(index, 1)
    }
  },
  mounted() {
    this.$refs.taskInput.focus()
  },
  updated() {
    this.$refs.taskInput.focus()
  }
}
</script>

<style scoped>
.list{
  width: 70vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.list h1 {
  text-align: center;
  color: #fff;
}

.form:not(3) {
  width: 450px;
  height: 50px;
  background: #FFF;
  display: flex;
  justify-content: center;
  align-items: center;
}

.form .input-data {
  margin: 0;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: 450px;
  height: 100%;
}

.form .input-data input {
  height: 100%;
  width: 70%;
  border: none;
  outline: none;
  font-size: 17px;
  border-bottom: 2px solid silver;
}

.form .input-data button {
  width: 6rem;
  height: 1.5rem;
  border-radius: 5px;
  color: #FFF;
  background-color: rgb(121, 121, 206);
  border: 1px solid blue;
  font-size: 1rem;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-style: bold;
  margin-left: 1rem;
  cursor: pointer;
}

.to-do-list{
  margin-top: 1rem;
  width: 70%;
  height: 70%;
  background-color: #FFF;
  overflow: auto;
  display: flex;
  justify-content: center;
}

.to-do-list ol {
  list-style: none;
  width: 80%;
}

.to-do-list ol li {
  padding: 5px;
  border-top: 1px solid #5300d8;
  display: flex;
  justify-content: space-between;
}

.to-do-list ol li .text {
  max-width: (100% - 60px);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.to-do-list ol li .text.completed {
  text-decoration: line-through;
}

.error-message {
  color: rgb(250, 40, 40);
  text-align: center;
  margin-bottom: 0;
  font-size: 1.3rem;
}

.text {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 1.2rem
}

.complete {
  background-color: #FFF;
  border: 2px solid green;
  margin-right: 0.3rem;
  cursor: pointer;
}

.remove {
  background-color: #FFF;
  border: 2px solid red;
  color: red;
  font-size: 15.5px;
  cursor: pointer;
}

</style>
