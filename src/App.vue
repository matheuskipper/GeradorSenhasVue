<template></template>

<script>
import generator from "generate-password-browser";

let password = generator.generate({
  length: 12,
  numbers: true,
});

console.log(password);
</script>

<style scoped></style>
