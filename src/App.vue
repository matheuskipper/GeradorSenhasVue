<template>
  <div
    class="flex flex-col items-center justify-center min-h-screen bg-gray-900 text-white p-4"
  >
    <h1 class="font-bold font-mono text-[35px] p-4">Generate Password</h1>
    <div
      class="w-full max-w-md p-6 bg-white rounded-lg shadow-lg text-gray-900"
    >
      <div class="p-4">
        <label for="password-length" class="block text-lg font-medium mb-2"
          >Password Size: {{ length }}</label
        >
        <input
          type="range"
          min="6"
          max="20"
          v-model="length"
          class="w-full mt-2 cursor-pointer"
        />
      </div>
      <div class="flex flex-col gap-4 mb-6">
        <label
          class="cursor-pointer flex items-center font-semibold"
          for="input-uppercase"
          ><input
            id="input-uppercase"
            class="cursor-pointer mr-2 w-6 h-6"
            type="checkbox"
            v-model="includeUppercase"
          />Include uppercase</label
        >
        <label
          class="cursor-pointer flex items-center font-semibold"
          for="input-numbers"
          ><input
            id="input-numbers"
            class="cursor-pointer mr-2 w-6 h-6"
            type="checkbox"
            v-model="includeNumbers"
          />Include numbers</label
        >
        <label
          class="cursor-pointer flex items-center font-semibold"
          for="input-symbols"
          ><input
            id="input-symbols"
            class="cursor-pointer mr-2 w-6 h-6"
            type="checkbox"
            v-model="includeSymbols"
          />Include symbols</label
        >
      </div>
      <button
        @click="generatePassword"
        class="bg-blue-500 hover:bg-blue-600 font-bold text-white px-4 py-3 rounded-lg shadow-md transition duration-300 cursor-pointer"
      >
        Generate
      </button>

      <div
        v-if="password"
        class="flex items-center justify-between mt-6 p-4 border border-yellow-500 bg-yellow-100 text-yellow-900 rounded-lg animate-fade-in"
      >
        <h1 class="text-lg font-bold tracking-wide">
          {{ password }}
        </h1>

        <button
          v-if="password"
          @click="copyPassword"
          class="bg-yellow-500 hover:bg-yellow-600 font-bold text-white px-4 py-2 rounded-lg cursor-pointer"
        >
          Copy
        </button>
      </div>
    </div>
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
import Toastify from "toastify-js";
import "toastify-js/src/toastify.css";

export default {
  data() {
    return {
      length: 6,
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
      navigator.clipboard.writeText(this.password).then(() => {
        Toastify({
          text: "Copied to clipboard!",
          duration: 2000,
          close: true,
          gravity: "bottom",
          position: "right",
          style: {
            background: "#7cb055",
            borderRadius: "8px",
          },
        }).showToast();
      });
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
