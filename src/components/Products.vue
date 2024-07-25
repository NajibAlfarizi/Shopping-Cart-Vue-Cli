<template>
  <div>
    <h1>Simple Shopping Cart</h1>
    <navbar
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle-slide="toggleSlider"
      @delete-item="deleteItem"
    ></navbar>
    <price-slider
      :sliderStatus="sliderStatus"
      :maximum="maximum"
      @update-maximum="updateMaximum"
    ></price-slider>
    <product-list
      :maximum="maximum"
      :products="products"
      @add-item="addItem"
    ></product-list>
  </div>
</template>

<script>
import ProductList from "./ProductList.vue";
import PriceSlider from "./PriceSlider.vue";
import Navbar from "./Navbar.vue";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "products",
  props: [
    "products",
    "maximum",
    "cart",
    "cartQty",
    "cartTotal",
    "sliderStatus",
    "sliderState",
  ],
  components: {
    Navbar,
    PriceSlider,
    ProductList,
  },
  methods: {
    toggleSlider: function () {
      this.$emit("toggle");
    },
    addItem: function (item) {
      this.$emit("add", item);
    },
    deleteItem: function (index) {
      this.$emit("delete", index);
    },
    updateMaximum: function (value) {
      this.$emit("update-maximum", value);
    }
  },
};
</script>
