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
            v-if="(card.column === 1 || card.column === 2 || card.column === 3) && showInputEdit === false"
        >
          Редактировать</button>
        <input
            v-if="showInputEdit"
            type="text"
            placeholder="Заголовок карточки-задачи"
        >
        <input
            v-if="showInputEdit"
            type="text"
            placeholder="Описание задачи"
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
        >
        <button
            v-if="showInputEdit"
            @click="showInputEdit = false"
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
      >
        Удалить</button>
      <button
          v-if="card.column === 1 && showInputEdit === false"
          @click="card.column=2"
      >
        Взять в работу</button>
      <button
          v-if="card.column === 2 && showInputEdit === false"
          @click="card.column=3"
      >
        Отдать на тестирование
      </button>
      <button
          v-if="card.column === 3 && showInputEdit === false"
          @click="card.column=4"
      >
        Завершить задачу
      </button>
      <button
          v-if="card.column === 3 && showInputEdit === false"
          @click="card.column=2"
      >
        Вернуть в работу
      </button>
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
      showInputEdit: false
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