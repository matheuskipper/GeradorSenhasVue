<template>
  <div class="min-h-screen flex items-center justify-center">
    <h1 class="font-bold">Generate Password</h1>
  </div>
</template>

<script>
import generator from "generate-password-browser";

let password = generator.generate({
  length: 12,
  numbers: true,
});

console.log(password);
</script>

<style scoped></style>
