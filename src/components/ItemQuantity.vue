<template>
  <div id="quantity">
    <button @click="$emit('reduce')">-</button>
    <p>{{ quantity }}</p>
    <button @click="$emit('increase')">+</button>
  </div>
</template>

<script>
export default {
  name: "ItemQuantity",
  props: ["quantity"]
};
</script>

<style>
#quantity {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}
#quantity p {
  font-size: 16px;
  font-weight: bold;
  min-width: 30px;
}
</style>
