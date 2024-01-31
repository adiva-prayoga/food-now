<script>
import { ref } from "vue";
import ButtonVariant from "./ButtonVariant.vue";
import Modal from "./Modal.vue";

export default {
  props: ["selectedPizza", "selectedSize", "selectedToppings", "totalPrice"],
  name: "PaymentSummary",
  components: {
    ButtonVariant,
    Modal,
  },
  setup() {
    const showModal = ref(false);

    function openModal() {
      showModal.value = true;
    }

    function close() {
      showModal.value = false;
    }

    return {
      openModal,
      showModal,
      close,
    };
  },
};
</script>

<template>
  <div class="payment-summary">
    <Modal v-if="showModal" @close="close">
      <template #title> Order Success </template>
      <template #body> Thank you </template>
    </Modal>

    <h1 class="payment-summary--title">Payment Summary</h1>
    <div class="payment-summary--content">
      <ul>
        <li v-if="selectedPizza">
          <span>{{ selectedPizza.name }}</span>
          <span>
            {{
              (selectedPizza.discount.is_active
                ? selectedPizza.discount.final_price
                : selectedPizza.price
              ).toFixed(2)
            }}
          </span>
        </li>
        <li v-if="selectedSize">
          <span>{{ selectedSize.name }}</span>
          <span>${{ selectedSize.extra_price.toFixed(2) }}</span>
        </li>
        <li v-for="topping in selectedToppings" :key="topping.id">
          <span>{{ topping.name }}</span>
          <span>${{ topping.price.toFixed(2) }}</span>
        </li>
      </ul>
    </div>
    <div class="payment-summary--price">
      <span>Total Price: </span>
      <span>${{ totalPrice.toFixed(2) }}</span>
    </div>
    <ButtonVariant @click.prevent="openModal" variant="primary">
      Order Now
    </ButtonVariant>
  </div>
</template>
