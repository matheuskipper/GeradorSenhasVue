<template>
  <div
    class="flex flex-col items-center justify-center min-h-screen bg-gray-900 text-white p-4"
  >
    <h1 class="font-bold">Generate Password</h1>
    <div>
      <label for="password-length">Password Size: {{ length }}</label>
      <input
        type="range"
        min="8"
        max="20"
        v-model="length"
        class="w-full mt-2"
      />
    </div>
    <div class="flex flex-col gap-2 mb-3">
      <label class="cursor-pointer" for="input-uppercase"
        ><input
          id="input-uppercase"
          class="cursor-pointer"
          type="checkbox"
          v-model="includeUppercase"
        />Include uppercase</label
      >
      <label class="cursor-pointer" for="input-numbers"
        ><input
          id="input-numbers"
          class="cursor-pointer"
          type="checkbox"
          v-model="includeNumbers"
        />Include numbers</label
      >
      <label class="cursor-pointer" for="input-symbols"
        ><input
          id="input-symbols"
          class="cursor-pointer"
          type="checkbox"
          v-model="includeSymbols"
        />include symbols</label
      >
    </div>
    <button
      @click="generatePassword"
      class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg cursor-pointer"
    >
      Generate
    </button>

    <h1>{{ password }}</h1>

    <button
      @click="copyPassword"
      class="bg-yellow-500 hover:bg-yellow-600 text-white px-4 py-2 rounded-lg cursor-pointer"
    >
      Copy
    </button>
  </div>
</template>

<script>
import generator from "generate-password-browser";

export default {
  data() {
    return {
      length: 8,
      includeUppercase: false,
      includeNumbers: true,
      includeSymbols: true,
      password: "",
    };
  },
  methods: {
    generatePassword() {
      this.password = generator.generate({
        length: this.length,
        numbers: this.includeNumbers,
        symbols: this.includeSymbols,
        uppercase: this.includeUppercase,
        lowercase: true,
        strict: true,
      });
    },
    copyPassword() {
      navigator.clipboard.writeText(this.password);
    },
  },
};
</script>

<style scoped></style>
