<template>
  <div id="fruiticious">
    <h2>List item</h2>
    <div class="list-item">
      <CartItem
        v-for="item in this.items"
        :item="item"
        :key="item.id"
        @update-cart="updateCart"
      />
    </div>

    <CartTotal
      :cart="this.cart"
      :total="this.total"
      :totalQuantity="totalQuantity"
      @empty-cart="emptyCart"
    />
  </div>
</template>

<script>
import CartItem from "./CartItem.vue";
import CartTotal from "./CartTotal.vue";

export default {
  name: "ShopCart",
  components: { CartItem, CartTotal },
  data() {
    return {
      items: [
        { id: 205, name: "Banana", price: 1 },
        { id: 148, name: "Orange", price: 2 },
        { id: 248, name: "Apple", price: 3 },
        { id: 260, name: "Mango", price: 4 },
      ],
      cart: [],
      total: 0,
      totalQuantity: 0,
    };
  },
  methods: {
    updateCart(item) {
      const existingItem = this.cart.find(
        (cartItem) => cartItem.id === item.id
      );

      if (existingItem) {
        existingItem.quantity += item.quantity;
        existingItem.total += item.quantity * item.price;
      } else {
        this.cart.push({ ...item, total: item.price * item.quantity });
      }

      this.total = this.cart.reduce(
        (total, cartItem) => total + cartItem.price * cartItem.quantity,
        0
      );

      this.totalQuantity = this.cart.reduce(
        (total, cartItem) => total + cartItem.quantity,
        0
      );
    },
    emptyCart() {
      this.cart = [];
      this.total = 0;
      this.totalQuantity = 0;
    },
  },
};
</script>

<style>
#fruiticious {
  display: flex;
  flex-flow: column;
  gap: 7px;
  width: 700px;
  margin: 0 auto;
}
.list-item {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 8px;
}
</style>
