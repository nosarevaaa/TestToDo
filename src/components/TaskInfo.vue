<template>
  <div class="task-info basic-list">
    <h2>Добавить задачу</h2>
    <input v-model="title" type="text"  placeholder="Название">
    <textarea v-model="description" placeholder="Описание задачи"></textarea>
    <div class="button-box">
      <button @click="emitOnCancel" type="reset">Отмена</button>
      <button @click="onAddTask" type="button">Сохранить</button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  emits: ['onAddTask', 'onCancel'],

  setup (props, { emit }) {
    const title = ref('')
    const description = ref('')

    const cancel = () => {
      title.value = ''
      description.value = ''
    }
        
    const onAddTask = () => {
      if (!title.value || !description.value) {
        alert('Заполните название и описание задачи')
      }
      else {
        emit('onAddTask', { title: title.value, description: description.value })
        cancel()
        emitOnCancel()
      }
    }

    const emitOnCancel = () => {
      cancel()
      emit('onCancel')
    }

    return {
      title,
      description,
      emitOnCancel,
      onAddTask
    }
  }
}
</script>

<style scoped>
  .task-info {
    width: 450px;
    padding: 20px;
    border-radius: 10px;
    background-color: white;
  }

  h2 {
    text-align: left;
  }

  textarea {
    height: 150px;
    resize: none;
  }

  .button-box {
    display: flex;
    justify-content: end;
    gap: 10px;
  }
</style>