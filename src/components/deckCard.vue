<template>
    <img :src="image" class="image" @click="onSubmit">
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const DeckCard = defineComponent({
  props: {
    image: String,
    id: Number,
  },
  methods: {
    onSubmit() {
      this.$emit('choseCard', this.id);
    },
  },
});

export default DeckCard;
</script>

<style src="./cardStyle.scss" lang="scss" scoped></style>
