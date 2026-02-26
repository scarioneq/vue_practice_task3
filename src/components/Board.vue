<template>
  <div class="board">
    <Column
        title="Запланированные задачи"
        :cards="cards.filter(card => card.column === 1)"
        @deleteCardEvent="$emit('deleteCardEvent', $event)"
        @editCardEvent="$emit('editCardEvent', $event)"
        @saveToLocalStorageEvent="$emit('saveToLocalStorageEvent', $event)"
    />
    <Column
        title="Задачи в работе"
        :cards="cards.filter(card => card.column === 2)"
        @editCardEvent="$emit('editCardEvent', $event)"
        @saveToLocalStorageEvent="$emit('saveToLocalStorageEvent', $event)"
    />
    <Column
        title="Тестирование"
        :cards="cards.filter(card => card.column === 3)"
        @editCardEvent="$emit('editCardEvent', $event)"
        @editColumnEvent="$emit('editColumnEvent', $event)"

    />
    <Column
        title="Выполненные задачи"
        :cards="cards.filter(card => card.column === 4)"
    />

  </div>
</template>

<script>
import Column from "@/components/Column.vue";

export default {
  components: {Column},
  props: {
    cards: {
      type: Array,
      required: true,
    }

  }

}
</script>

<style>

.board {
  display: flex;
  justify-content: space-between;
}

</style>