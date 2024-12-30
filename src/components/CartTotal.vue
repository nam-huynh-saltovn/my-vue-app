<template>
  <div class="cart">
    <h2>Fruiticious cart</h2>
    <table id="cart-table">
      <tr>
        <th>Name</th>
        <th>price</th>
        <th>quantity</th>
        <th>total</th>
      </tr>

      <tr v-for="item in cart" :key="item.id">
        <td>{{ item.name }}</td>
        <td>${{ item.price }}</td>
        <td>{{ item.quantity }}</td>
        <td>${{ item.total }}</td>
      </tr>

      <tr class="total">
        <td colspan="2">Total:</td>
        <td>{{ totalQuantity }}</td>
        <td>
          <strong id="total-money">${{ total }}</strong>
        </td>
      </tr>
      <tr></tr>
    </table>
    <button @click="$emit('empty-cart')">Empty cart</button>
  </div>
</template>

<script>
export default {
  name: "CartTotal",
  props: ["cart", "total", "totalQuantity"],
  data() {
    return {};
  },
};
</script>

<style>
.cart {
  border-radius: 10px;
  background-color: cadetblue;
  padding: 5px;
}

#cart-table {
  width: 100%;
}

#cart-table th,
td {
  border: 1px solid;
}

#cart-table tr {
  background-color: #f2f2f2;
}

#cart-table th {
  text-align: left;
  background-color: #04aa6d;
  color: white;
}

#total-money {
  color: red;
}
</style>
