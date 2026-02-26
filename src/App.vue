<template>
  <div class="app-container">
    <h1>Канбан-доска</h1>
    <div>
      <form class="form-inline"
        @submit.prevent
      >
        <button
            @click="showInput = true"
            v-if="!showInput"
        >
          Создать карточку задачи (в первом столбце)
        </button>
        <div

        >
          <input
              v-if="showInput"
              v-model="card.title"
              type="text"
              placeholder="Заголовок карточки-задачи"
          >
          <input
              v-if="showInput"
              v-model="card.textTask"
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
              v-model="card.deadlineDate"
              type="date"
          >
          <button
              v-if="showInput"
              @click="[showInput = false, createCard()]"
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
      card : {
        title: '',
        textTask: '',
        deadlineDate: '',
      },

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
  },
  methods: {
    formatDate() {
      const d = new Date();
      const day = d.getDate().toString().padStart(2, '0');
      const month = (d.getMonth() + 1).toString().padStart(2, '0');
      const year = d.getFullYear();

      return `${day}.${month}.${year}`;
    },

    createCard() {

      if (this.card.title && this.card.textTask && this.card.deadlineDate) {
        const card = {
          id: this.cards.length + 1,
          title: this.card.title,
          column: 1,
          textTask: this.card.textTask,
          reasonForReturn: '',
          deadlineExpired: '',
          deadlineDate: this.card.deadlineDate,
          createdAt: this.formatDate(),
          updatedAt: ''
        }
        this.cards.push(card);

      } else {
        alert("Заполните заголовок, описание и крайний срок выполнения карточки")
      }
    }
  },
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

.form-inline div {
  display: inline-flex;
  flex-direction: column;
}

.form-inline button {
  background: none;
  border-radius: 2px;
  border: 1px solid teal;
  padding: 3px;
  transition: background-color 0.3s ease;
  margin-bottom: 5px;
}

.form-inline button:hover {
  box-shadow: 2px 4px 10px;
  padding: 10px 10px;
  border: none;
  cursor: pointer;
  background: teal;
  border-radius: 2px;
  margin-top: 5px;
}

.form-inline input {
  background: none;
  border-radius: 2px;
  border: 1px solid teal;
  padding: 3px;
  transition: background-color 0.3s ease;
  margin-bottom: 5px;
}

.form-inline input:focus {
  background: none;
  box-shadow: 2px 4px 10px;
  border: 1px solid teal;
  border-radius: 2px;
  margin-top: 5px;
}

</style>