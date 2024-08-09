<template>
  <header>
    <h1>ToDo App</h1>
  </header>
  <main>
    <ul class="task-list basic-list">
      <li>
        <button @click="switchVisible" class="add-button" type="button">Добавить задачу</button>
      </li>
      <li v-for="item in taskList" :key="item.id">
        <TaskCard @onRemove="removeTask(item.id)" @onDone="setDoneTask(item.id)" :model="item"></TaskCard>
      </li>
    </ul>
    <div v-show="isVisible" class="popup-wrapper">
      <TaskInfo @onAddTask="addTask" @onCancel="switchVisible"></TaskInfo>
    </div>
  </main>
  <footer>
    <p>Данное приложение было реализовано в рамках тестового задания для вакансии <a href="https://tomsk.hh.ru/vacancy/105294699" target="_blank">"Начинаюший Web-программист / разработчик"</a></p>
    <p>С моим резюме можно ознакомиться по ссылке <a href="https://tomsk.hh.ru/resume/cf92671bff0d5424050039ed1f6d707457736a" target="_blank">Резюме</a></p>
  </footer>
</template>

<script>
import TaskCard from './components/TaskCard.vue';
import TaskInfo from './components/TaskInfo.vue';
import {ref} from 'vue'

export default {
  name: 'App',
  components: {
    TaskCard,
    TaskInfo
  },

  setup() {
    const taskList = ref([{id: 0, title: "Название задачи", description: "Описание задачи", isDone: false}])
    const isVisible = ref(false)

    const addTask = ({title, description}) => {
      taskList.value = [... taskList.value, {id: taskList.value[taskList.value.length - 1].id + 1, title, description, isDone: false}]
      switchVisible
    }

    const switchVisible = () => {
      isVisible.value = !isVisible.value
    }

    const setDoneTask = (id) => {
      taskList.value = taskList.value.map(item => {
        if(item.id == id)
          item.isDone = true
        return item
      })
    }

    const removeTask = (id) => {
      taskList.value = taskList.value.filter(item => item.id !== id)
    }

    return {
      isVisible,
      taskList,
      addTask,
      removeTask,
      setDoneTask,
      switchVisible
    }
  }
}


</script>

<style scoped>
  header {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 70px;

    color: white;
    font-weight: bold;

    background-color: cornflowerblue;
  }

  main {
    margin: 0 auto;
    max-width: 800px;
    min-height: calc(100vh - 370px);
  }

  .add-button {
    width: 100%;
    text-align: center;
  }

  .task-list {
    padding-block: 20px;
    list-style: none;
  }

  .popup-wrapper {
    position: fixed;
    top: 0;
    left: 0;

    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
    height: 100vh;

    background-color: rgba(0,0,0,0.5);
  }

  footer {
    padding-block: 70px;
    height: 300px;
    background-color: cornflowerblue;
    color: white;
    font-weight: bold;
  }

  a {
    color: white;
    text-decoration: underline;
  }
</style>