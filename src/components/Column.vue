<template>
  <div class="div-column">
    <div>
      <h2>{{ title }}</h2>
    </div>
    <div>
      Всего задач: {{ cards.length }}
    </div>
    <Card
        v-for="card in cards"
        :key="card.id"
        :card="card"
        @deleteCardEvent="$emit('deleteCardEvent', $event)"
        @editCardEvent="$emit('editCardEvent', $event)"
        @editColumnEvent="$emit('editColumnEvent', $event)"
        @saveToLocalStorageEvent="$emit('saveToLocalStorageEvent', $event)"
    />


  </div>
</template>

<script>
import Card from "@/components/Card.vue";

export default {
  components: {Card},
  props: {
    title: {
      type: String,
      required: true
    },
    cards: {
      type: Array,
      required: true,
    }
  }

}
</script>

<style>

.div-column {
  padding: 10px;
  border: 1px solid #292828;
  background-color: #ebe6ed;
  border-radius: 5px;

}

h2 {
  color: #201c1c;
}

div {
  color: #201c1c;
}

</style>