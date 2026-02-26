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
        @deleteCardEvent="deleteCard"
        @editCardEvent="editCard"
        @editColumnEvent="editCardColumn"
        @saveToLocalStorageEvent="saveToLocalStorage"
    />

  </div>

</template>

<script>
import Board from "@/components/Board.vue";

export default {
  created() {
    this.loadFromLocalStorage()
  },
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
          deadlineDate: '2026-03-02',
          createdAt: '2026-02-25',
          updatedAt: '',
        },
        {
          id: 2,
          title: 'Написать сервис авторизации',
          column: 2,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: '',
          deadlineDate: '2026-03-02',
          createdAt: '2026-02-24',
          updatedAt: '',
        },
        {
          id: 3,
          title: 'Написать сервис выдачи ролей',
          column: 3,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: '',
          deadlineDate: '2026-03-02',
          createdAt: '2026-02-24',
          updatedAt: '2026-02-18',
        },
        {
          id: 4,
          title: 'Написать сервис авторизации',
          column: 4,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: false,
          deadlineDate: 'Poka tak2',
          createdAt: '2026-02-22',
          updatedAt: '2026-02-18',
        },
        {
          id: 5,
          title: 'Подключить Google OAuth',
          column: 4,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: true,
          deadlineDate: '2026-02-23',
          createdAt: '2026-02-18',
          updatedAt: '2026-02-18',
        },
        {
          id: 6,
          title: 'Подключить VK Oauth',
          column: 2,
          textTask: 'Чтобы без багов',
          reasonForReturn: 'Много багов!!!',
          deadlineExpired: '',
          deadlineDate: '2026-02-29',
          createdAt: '2026-02-18',
          updatedAt: '2026-02-19',
        },
        {
          id: 7,
          title: 'Написать сервис выдачи ролей',
          column: 3,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: '',
          deadlineDate: '2026-02-02',
          createdAt: '2026-02-24',
          updatedAt: '2026-02-18',
        },
        {
          id: 8,
          title: 'Написать сервис выдачи ролей',
          column: 3,
          textTask: 'Чтобы без багов',
          reasonForReturn: '',
          deadlineExpired: '',
          deadlineDate: '2026-02-26',
          createdAt: '2026-02-24',
          updatedAt: '2026-02-18',
        },

      ]
    }
  },
  methods: {
    loadFromLocalStorage() {
      const savedCards = localStorage.getItem('cards')

      if (savedCards) {
        this.cards = JSON.parse(savedCards)
      }

    },
    saveToLocalStorage() {
      localStorage.setItem('cards', JSON.stringify(this.cards))
    },

    formatDate() {
      const d = new Date();
      const day = d.getDate().toString().padStart(2, '0');
      const month = (d.getMonth() + 1).toString().padStart(2, '0');
      const year = d.getFullYear();

      return `${year}-${month}-${day}`;
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
        this.saveToLocalStorage()

      } else {
        alert("Заполните заголовок, описание и крайний срок выполнения карточки")
      }
    },
    deleteCard(data) {
       this.cards = this.cards.filter(c => c.id !== data.card.id)
      this.saveToLocalStorage()
    },
    editCard(data) {
      this.cards[data.card.id-1].title = data.cardEdit.title
      this.cards[data.card.id-1].textTask = data.cardEdit.textTask
      this.cards[data.card.id-1].deadlineDate = data.cardEdit.deadlineDate
      this.cards[data.card.id-1].updatedAt = this.formatDate()
      this.saveToLocalStorage()
      data.cardEdit.title = ''
      data.cardEdit.taskText = ''
      data.cardEdit.deadlineDate = ''
    },
    editCardColumn(data) {

      if ((data.editNumColumn === 2 && data.cardEdit.reasonForReturn) || data.editNumColumn === 4) {
        this.cards[data.card.id-1].column = data.editNumColumn
        this.cards[data.card.id-1].reasonForReturn = data.cardEdit.reasonForReturn
        this.saveToLocalStorage()
      } else {
        alert("Заполните причину возврата карточки в работу")
      }
      if (data.editNumColumn === 4) {
        const deadline = new Date(data.card.deadlineDate);
        const today = new Date(this.formatDate());

        this.cards[data.card.id-1].column = data.editNumColumn
        this.cards[data.card.id-1].deadlineExpired = deadline < today;
        this.saveToLocalStorage()

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