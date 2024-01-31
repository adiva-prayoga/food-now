<script>
import { ref, watch } from "vue";
import PaymentSummary from "./PaymentSummary.vue";

export default {
  props: ["sizes", "pizzas", "toppings"],
  setup(props) {
    const selectedPizza = ref(null);
    const selectedSize = ref(null);
    const selectedToppings = ref([]);
    const totalPrice = ref(0);

    const updateTotalPrice = () => {
      let pizzaPrice = selectedPizza.value?.discount?.final_price || 0;
      let sizePrice = selectedSize.value?.extra_price || 0;
      let toppingsPrice = selectedToppings.value.reduce(
        (total, topping) => total + topping.price,
        0
      );

      totalPrice.value = pizzaPrice + sizePrice + toppingsPrice;
    };

    const pizzaImagePath = (pizza) => {
      return `/assets/${pizza.name}.png`;
    };

    const finalPrice = (pizza) => {
      return pizza.discount.is_active
        ? pizza.discount.final_price.toFixed(2)
        : pizza.price.toFixed(2);
    };

    watch([selectedPizza, selectedSize, selectedToppings], updateTotalPrice);

    watch(selectedPizza, () => {
      selectedSize.value = props.sizes.find((size) => size.name === "Small");
      selectedToppings.value = [];
    });

    return {
      selectedPizza,
      selectedSize,
      selectedToppings,
      totalPrice,
      updateTotalPrice,
      pizzaImagePath,
      finalPrice,
      sizes: props.sizes,
      pizzas: props.pizzas,
      toppings: props.toppings,
    };
  },
  name: "OrderForm",
  components: {
    PaymentSummary,
  },
};
</script>

<template>
  <section class="order-section container">
    <form @change="updateTotalPrice">
      <div class="order-section--wrapper">
        <div class="order-section--wrapper--pizza">
          <h1 class="order-section--wrapper--pizza--title">
            Choose your pizza
          </h1>
          <!-- Pizza options -->
          <div class="pizza-options">
            <label
              v-for="pizza in pizzas"
              :key="pizza.id"
              class="pizza-label"
              :class="{ 'selected-pizza': selectedPizza === pizza }"
            >
              <input
                class="hidden-radio"
                type="radio"
                v-model="selectedPizza"
                :value="pizza"
                name="pizza"
              />

              <div class="pizza-options--content">
                <img class="pizza-image" :src="pizzaImagePath(pizza)" />

                <div :class="{ 'selected-pizza': selectedPizza === pizza }">
                  <p>
                    {{ pizza.name }}
                  </p>
                  <span class="final-price"> ${{ finalPrice(pizza) }} </span>

                  <span
                    v-show="pizza.discount.is_active"
                    class="full-price"
                    :class="{ strikethrough: pizza.discount.is_active }"
                  >
                    ${{ pizza.price.toFixed(2) }}
                  </span>
                </div>
              </div>

              <img
                class="ribbon"
                v-if="pizza.discount.is_active"
                src="/assets/ribbon.svg"
              />
            </label>
          </div>
        </div>

        <div class="order-section--wrapper--custom-pizza">
          <h1 class="order-section--wrapper--custom-pizza--title">
            Custom Pizza
          </h1>
          <!-- Size options -->
          <div class="size-options">
            <h2 class="size-options--title">Size</h2>
            <div class="size-options--wrapper">
              <div v-for="size in sizes" :key="size.id">
                <input
                  class="hidden-radio"
                  type="radio"
                  v-model="selectedSize"
                  :value="size"
                  name="size"
                  :disabled="!selectedPizza"
                  :id="`size-${size.id}`"
                />
                <label :for="`size-${size.id}`">
                  <p>
                    {{ size.name }}<span>({{ size.extra_price }}$)</span>
                  </p>
                </label>
              </div>
            </div>
          </div>

          <!-- Toppings options -->
          <div class="toppings-options">
            <h2 class="toppings-options--title">Toppings</h2>
            <div class="toppings-options--list">
              <label
                v-for="topping in toppings"
                :key="topping.id"
                :for="`topping-${topping.id}`"
                class="custom-checkbox"
                :class="{
                  'checkbox-checked': selectedToppings.includes(topping),
                  'checkbox-disabled':
                    !selectedPizza ||
                    (selectedPizza &&
                      !selectedPizza.toppings.includes(topping.id)),
                }"
              >
                <input
                  class="hidden-checkbox"
                  type="checkbox"
                  :value="topping"
                  v-model="selectedToppings"
                  :disabled="
                    !selectedPizza ||
                    (selectedPizza &&
                      !selectedPizza.toppings.includes(topping.id))
                  "
                  :id="`topping-${topping.id}`"
                />
                {{ topping.name }}
              </label>
            </div>
          </div>
        </div>
      </div>

      <PaymentSummary
        :selectedPizza="selectedPizza"
        :selectedSize="selectedSize"
        :selectedToppings="selectedToppings"
        :totalPrice="totalPrice"
      />
    </form>
  </section>
</template>
