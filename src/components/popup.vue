<template>
<div class="popupPosition">
    <div class="popupWrapper">
        <h2>{{mesage}}</h2>
        <p>{{description}}</p>
        <button class="popupButton" @click="onClick">Play</button>
    </div>
</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const Popup = defineComponent({
  props: {
    mesage: String,
    description: String,
  },
  methods: {
    onClick() {
      this.$emit('closePopup', false);
    },
  },
});

export default Popup;
</script>

<style src="./cardStyle.scss" lang="scss" scoped></style>
