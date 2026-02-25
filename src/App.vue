<template>
  <div class="app-container">
    <h1>Канбан-доска</h1>
    <div>
      <form
        @submit.prevent
      >
        <button
            @click="showInput = true"
            v-if="!showInput"
        >
          Создать карточку задачи (в первом столбце)
        </button>
        <div>
          <input
              v-if="showInput"
              type="text"
              placeholder="Заголовок карточки-задачи"
          >
          <input
              v-if="showInput"
              type="text"
              placeholder="Описание задачи"
          >
          <button
              v-if="showInput"
              @click="showInput = false"
          >
            Создать</button>
          <button
              v-if="showInput"
              @click="showInput = false"
          >
            Отмена создания</button>

        </div>
      </form>
    </div>


  </div>
</template>

<script>
export default {
  data() {
    return {
      showInput: false,
    }
  }

}
</script>

<style>

</style>