<script>
import { ref } from "vue";
import OrderForm from "./OrderForm.vue";
import sizeList from "../utils/size-list.json";
import pizzaList from "../utils/pizza-list.json";
import toppingList from "../utils/topping-list.json";

export default {
  name: "OrderPizza",
  components: {
    OrderForm,
  },
  setup() {
    const sizes = ref(sizeList.data);
    const pizzas = ref(pizzaList.data);
    const toppings = ref(toppingList.data);

    return {
      sizes,
      pizzas,
      toppings,
    };
  },
};
</script>

<template>
  <OrderForm :sizes="sizes" :pizzas="pizzas" :toppings="toppings" />
</template>
