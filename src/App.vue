<template>
  <div
    class="flex flex-col items-center justify-center min-h-screen bg-gray-900 text-white p-4"
  >
    <h1 class="font-bold text-[35px] p-4">Generate Password</h1>
    <div class="p-4">
      <label for="password-length">Password Size: {{ length }}</label>
      <input
        type="range"
        min="8"
        max="20"
        v-model="length"
        class="w-full mt-2 cursor-pointer"
      />
    </div>
    <div class="flex flex-col gap-2 mb-3 p-2">
      <label class="cursor-pointer flex items-center" for="input-uppercase"
        ><input
          id="input-uppercase"
          class="cursor-pointer mr-2 w-5 h-5"
          type="checkbox"
          v-model="includeUppercase"
        />Include uppercase</label
      >
      <label class="cursor-pointer flex items-center" for="input-numbers"
        ><input
          id="input-numbers"
          class="cursor-pointer mr-2 w-5 h-5"
          type="checkbox"
          v-model="includeNumbers"
        />Include numbers</label
      >
      <label class="cursor-pointer flex items-center" for="input-symbols"
        ><input
          id="input-symbols"
          class="cursor-pointer mr-2 w-5 h-5"
          type="checkbox"
          v-model="includeSymbols"
        />Include symbols</label
      >
    </div>
    <button
      @click="generatePassword"
      class="bg-blue-500 hover:bg-blue-600 font-bold text-white px-4 py-2 rounded-lg cursor-pointer"
    >
      Generate
    </button>

    <div
      v-if="password"
      class="mt-4 p-4 border border-yellow-500 bg-yellow-100 text-yellow-900 rounded-lg animate-fade-in"
    >
      <h1 class="text-lg font-bold tracking-wide">{{ password }}</h1>
    </div>

    <button
      v-if="password"
      @click="copyPassword"
      class="bg-yellow-500 hover:bg-yellow-600 font-bold text-white px-4 py-2 rounded-lg cursor-pointer mt-4"
    >
      Copy
    </button>
  </div>
  <footer class="bg-gray-600 text-white p-3">
    <p class="text-center text-sm">
      Developed by
      <a target="_blank" href="https://github.com/matheuskipper"
        >Matheus Kipper</a
      >
    </p>
  </footer>
</template>

<script>
import generator from "generate-password-browser";

export default {
  data() {
    return {
      length: 8,
      includeUppercase: false,
      includeNumbers: false,
      includeSymbols: false,
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

<style scoped>
@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.animate-fade-in {
  animation: fade-in 0.5s ease-in-out;
}
</style>
