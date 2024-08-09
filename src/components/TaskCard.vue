<template>
  <div class="task-card basic-item">
    <div>
      <h2>{{ model.title }}</h2>
      <p>{{ model.description }}</p>
    </div>
    <div>
      <button @click="emitOnDone" v-if="!model.isDone" type="reset">✅</button>
      <button @click="emitOnRemove" v-else type="reset">❌</button>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['onDone', 'onRemove'],  
  props: {
    model: {
      required: true,
      default: {
        id: 0,
        title: "Название задачи",
        description: "Описание задачи",
        isDone: false
      }
    }
  },

  setup (props, { emit }) {
    const emitOnDone = () => {
      emit('onDone')  
    }
    
    const emitOnRemove = () => {
      emit('onRemove')  
    } 

    return {
      emitOnDone,
      emitOnRemove
    }
  }
}
</script>

<style scoped>
  .task-card {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h2, p {
    text-align: left;
    padding-right: 20px;
  }
</style>