<script>
import { defineComponent } from "vue";
import ButtonVariant from "./ButtonVariant.vue";

export default defineComponent({
  name: "Modal",
  props: {
    show: {
      type: Boolean,
      required: true,
    },
  },
  components: {
    ButtonVariant,
  },
});
</script>

<style scoped>
.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
}
</style>

<template>
  <div class="modal">
    <div class="modal--content">
      <img src="/assets/modal.svg" alt="" />
      <h2>Order Success</h2>
      <p>Thank you, we have received your order successfully.</p>
    </div>
  </div>
</template>
