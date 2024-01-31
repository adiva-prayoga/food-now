<script>
import OrderForm from "./OrderForm.vue";
import sizeList from "../utils/size-list.json";
import pizzaList from "../utils/pizza-list.json";
import toppingList from "../utils/topping-list.json";

export default {
  data() {
    return {
      sizes: sizeList.data,
      pizzas: pizzaList.data,
      toppings: toppingList.data,
    };
  },
  name: "OrderPizza",
  components: {
    OrderForm,
  },
};
</script>

<template>
  <OrderForm :sizes="sizes" :pizzas="pizzas" :toppings="toppings" />
</template>
