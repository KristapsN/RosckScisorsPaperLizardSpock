<template>
  <div class="cardWrapper"  @click="onSubmit">
      <img :src="image" class="image">
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const DeckCard = defineComponent({
  components: {
  },
  props: {
    icon: String,
    image: String,
    id: Number,
  },
  data() {
    return {
    };
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
