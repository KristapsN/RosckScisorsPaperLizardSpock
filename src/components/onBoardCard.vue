<template>
      <img :src="image" class="image imageOnBoard">
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const OnBoardCard = defineComponent({
  components: {
  },
  props: {
    image: String,
    id: Number,
  },
  data() {
    return {
    };
  },
});

export default OnBoardCard;
</script>

<style src="./cardStyle.scss" lang="scss" scoped></style>
