<template>
  <div id="basecard">
    <slot></slot>
  </div>
</template>

<style scoped>
div#basecard {
  margin: 2rem auto;
  max-width: 40rem;
  padding: 1 rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  text-align: center;
  background-color: rgb(134 25 143);
}
</style>
