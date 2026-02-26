<template>
  <div class="div-card">
    <div>
      <h3>{{ card.title }}</h3>
      <p>Создано: {{ card.createdAt }}</p>
    </div>
    <div class="card">
      <h4>Описание задачи:</h4>
      <p>{{ card.textTask }}</p>
      <h5 class="deadline-srok">Крайний срок выполнения:</h5>
      <p>{{ card.deadlineDate }}</p>
      <h5
          v-if="card.reasonForReturn"
      >
        Причина возврата в работу:
      </h5>
      <p>{{ card.reasonForReturn }}</p>
      <p v-if="card.deadlineExpired" class="prosrok">Просрочена</p>
      <p v-if="card.deadlineExpired === false" class="normsrok">Сдана в срок</p>
    </div>
    <p v-if="card.updatedAt">Редактировано: {{ card.updatedAt }}</p>
    <div class="btn-card">
      <div class="form-inline-card btn-card">
        <button
            @click="showInputEdit = true"
            v-if="(card.column === 1 || card.column === 2 || card.column === 3) && showInputEdit === false && showInputReasonForReturn === false"
        >
          Редактировать</button>
        <input
            v-if="showInputEdit"
            type="text"
            placeholder="Заголовок карточки-задачи"
            v-model="cardEdit.title"
        >
        <input
            v-if="showInputEdit"
            type="text"
            placeholder="Описание задачи"
            v-model="cardEdit.textTask"
        >
        <label
            for="dateDeadline"
            v-if="showInputEdit"
        >
          Крайний срок выполнения:
        </label>
        <input
            id="dateDeadline"
            v-if="showInputEdit"
            type="date"
            v-model="cardEdit.deadlineDate"
        >
        <button
            v-if="showInputEdit"
            @click="[showInputEdit = false, editCard()]"
        >
          Редактировать
        </button>
        <button
            v-if="showInputEdit"
            @click="showInputEdit = false"
        >
          Отмена редактирования
        </button>
      </div>

      <button
          v-if="card.column === 1 && showInputEdit === false"
          @click="deleteCard"
      >
        Удалить</button>
      <button
          v-if="card.column === 1 && showInputEdit === false"
          @click="[card.column=2, saveToLocalStorage()]"
      >
        Взять в работу</button>
      <button
          v-if="card.column === 2 && showInputEdit === false"
          @click="[card.column=3, card.reasonForReturn = '', saveToLocalStorage()]"
      >
        Отдать на тестирование
      </button>
      <button
          v-if="card.column === 3 && showInputEdit === false && showInputReasonForReturn === false"
          @click="editColumn(4)"
      >
        Завершить задачу
      </button>
      <div>
        <button
            v-if="card.column === 3 && showInputEdit === false && showInputReasonForReturn === false"
            @click="[showInputReasonForReturn = true]"

        >
          Вернуть в работу
        </button>
        <button
            v-if="showInputReasonForReturn === true"
            @click="[editColumn(2), showInputReasonForReturn = false]"
        >Вернуть в работу</button>
        <br>
        <input
            v-if="showInputReasonForReturn === true"
            type="text"
            placeholder="Причина возврата в работу"
            v-model="cardEdit.reasonForReturn"
        >
      </div>

    </div>

  </div>
</template>

<script>
export default {
  props: {
    card: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showInputEdit: false,
      showInputReasonForReturn: false,
      cardEdit : {
        title: '',
        textTask: '',
        deadlineDate: '',
        column: '',
        reasonForReturn: ''
      },
    }
  },
  methods: {
    deleteCard() {
      this.$emit('deleteCardEvent', {
        card: this.card,
      })
    },
    editCard() {
      if (!this.cardEdit.title) {
        this.cardEdit.title = this.card.title
      }
      if (!this.cardEdit.textTask) {
        this.cardEdit.textTask = this.card.textTask
      }
      if (!this.cardEdit.deadlineDate) {
        this.cardEdit.deadlineDate = this.card.deadlineDate
      }
      this.$emit('editCardEvent', {
        card: this.card,
        cardEdit: this.cardEdit
      })
    },
    editColumn(editNumColumn) {
      this.$emit('editColumnEvent', {
        card: this.card,
        cardEdit: this.cardEdit,
        editNumColumn: editNumColumn,

      })
    },
    saveToLocalStorage() {
      this.$emit('saveToLocalStorageEvent')
    }
  }

}
</script>

<style>

.div-card {
  padding: 10px;
  display: inline;
}

.card {
  border: 1px solid teal;
}

p {
  margin-bottom: 5px;
}

.prosrok {
  color: red;
}

.normsrok {
  color: teal;
}

.deadline-srok {
  color: #b32222;
}
.btn-card {
  display: flex;
  justify-content: space-between;

}

.btn-card button{
  background: none;
  border-radius: 2px;
  margin-top: 5px;
  border: 1px solid teal;
  padding: 3px;
  transition: background-color 0.3s ease;
}

.btn-card button:hover{
  box-shadow: 2px 4px 10px;
  padding: 10px 10px;
  border: none;
  cursor: pointer;
  background: teal;
  border-radius: 2px;
  margin-top: 5px;
}

.form-inline-card{
  display: flex;
  flex-direction: column;
}

.btn-card input {
  background: none;
  border-radius: 2px;
  border: 1px solid teal;
  padding: 3px;
  transition: background-color 0.3s ease;
  margin-bottom: 5px;
  margin-top: 5px;
}

.btn-card input:focus {
  background: none;
  box-shadow: 2px 4px 10px;
  border: 1px solid teal;
  border-radius: 2px;
  margin-top: 5px;
}




</style>