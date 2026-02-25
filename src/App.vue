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
        <div
            class="form-inline"
        >
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
          <label
              for="dateDeadline"
              v-if="showInput"
          >
            Крайний срок выполнения:
          </label>
          <input
              id="dateDeadline"
              v-if="showInput"
              type="date"
          >
          <button
              v-if="showInput"
              @click="showInput = false"
          >
            Создать
          </button>
          <button
              v-if="showInput"
              @click="showInput = false"
          >
            Отмена создания
          </button>
        </div>
      </form>
    </div>
    <Board
        :cards="cards"
    />

  </div>

</template>

<script>
import Board from "@/components/Board.vue";

export default {
  components: {Board},
  data() {
    return {
      showInput: false,
      cards: [
        {
          id: 1,
          title: 'Написать сервис подсчёта гостей',
          column: 1,
          //text
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          //boolean
          deadlineExpired: '',
          //date
          deadlineDate: '02.03.2026',
          createdAt: '25.02.2026',
          updatedAt: '',
        },
        {
          id: 2,
          title: 'Написать сервис авторизации',
          column: 2,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: '',
          deadlineDate: '02.03.2026',
          createdAt: '24.02.2026',
          updatedAt: '',
        },
        {
          id: 3,
          title: 'Написать сервис выдачи ролей',
          column: 3,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: '',
          deadlineDate: '02.03.2026',
          createdAt: '24.02.2026',
          updatedAt: '18.02.2026',
        },
        {
          id: 4,
          title: 'Написать сервис авторизации',
          column: 4,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: false,
          deadlineDate: 'Poka tak2',
          createdAt: '22.02.2026',
          updatedAt: '18.02.2026',
        },
        {
          id: 5,
          title: 'Подключить Google OAuth',
          column: 4,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: true,
          deadlineDate: '23.02.2026',
          createdAt: '18.02.2026',
          updatedAt: '18.02.2026',
        },
        {
          id: 6,
          title: 'Подключить VK Oauth',
          column: 2,
          textTask: 'Чтобы без багов',
          reasonForReturn: 'Много багов!!!',
          deadlineExpired: '',
          deadlineDate: '29.02.2026',
          createdAt: '18.02.2026',
          updatedAt: '19.02.2026',
        },

      ]
    }
  }

}
</script>

<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app-container {
  padding: 20px;
}

h1 {
  color: #252525;
}

.form-inline {
  display: flex;
  flex-direction: column;
}

</style>