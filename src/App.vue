<template>
  <div
    class="flex h-screen w-full flex-col items-center justify-center gap-2 selection:bg-amber-700 selection:text-amber-50"
  >
    <h1 class="text-4xl font-medium text-amber-900">Электронный дневник</h1>

    <div v-if="!auth"
      class="mt-8 flex h-max min-w-xl flex-col rounded-2xl border border-white bg-white p-5 transition-all hover:shadow-sm"
    >
      <form class="flex flex-col gap-4" @submit.prevent="viewPasswordVisible">
        <label class="flex flex-col gap-2">
          <span class="after:ml-0.5 after:text-red-500 after:content-['*']"
            >Email</span
          >
          <input  
            class="rounded-xl border border-amber-500 px-4 py-2 text-xl focus:outline-amber-600"
            type="email"
            placeholder="Email"
            v-model="formEmail"
            required
          />
        </label>
        <label class="flex flex-col gap-2">
          <span class="after:ml-0.5 after:text-red-500 after:content-['*']"
            >Пароль</span
          >
          <input
            class="rounded-xl border border-amber-500 px-4 py-2 text-xl focus:outline-amber-600"
            :type="viewPassword ? 'text' : 'password'"
            placeholder="Пароль"
            v-model="formPassword"
            required
          />
        </label>
        <div class="flex gap-2 text-xl select-none">
          <input
            class="ml-1 scale-150 accent-amber-700"
            type="checkbox"
            name="view-password"
            id="view-password"
            v-model="viewPassword"
          />
          <label for="view-password">{{
            viewPassword ? "Скрыть пароль" : "Показать пароль"
          }}</label>
        </div>
        <input
          class="cursor-pointer rounded-xl bg-amber-700 px-4 py-2 text-2xl text-amber-50 transition-colors hover:bg-amber-600"
          type="submit"
          value="Войти"
        />
      </form>
    </div>

    <div v-else>
      <h2>Вы вошли</h2>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const auth = ref(false);
const viewPassword = ref(false);

const formEmail = ref('')
const formPassword = ref('')

const viewPasswordVisible = () => {
  document.cookie = `${formEmail.value}=${formPassword.value}`;

  location.reload()
}

onMounted(() => {
  console.log(document.cookie);

  if (document.cookie) {
    console.log("Вы авторизованы");
    auth.value = true
  }
})
</script>