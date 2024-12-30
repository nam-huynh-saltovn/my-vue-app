<template>
  <div class="item">
    <div class="item-detail">
      <p>
        <strong>{{ item.name }}</strong>
      </p>
      <p>
        Price: <strong>${{ item.price }}</strong>
      </p>
    </div>
    <ItemQuantity
      :quantity="this.quantity"
      @reduce="reduce"
      @increase="increase"
    />
    <button class="Button" @click="addToCart(item)">Add To Cart</button>
  </div>
</template>

<script>
import ItemQuantity from "./ItemQuantity.vue";

export default {
  components: { ItemQuantity },
  name: "Cart-Item",
  props: ["item"],
  data() {
    return {
      quantity: 1,
    };
  },
  methods: {
    addToCart(item) {
      this.$emit("update-cart", { ...item, quantity: this.quantity });
      this.quantity = 1;
    },
    reduce() {
      if (this.quantity > 1) this.quantity--;
    },
    increase() {
      this.quantity++;
    },
  },
};
</script>

<style>
.item {
  display: flex;
  justify-content: space-around;
  align-items: center;
  border: 1px solid;
  border-radius: 5px;
  margin-bottom: 5px;
}
</style>
