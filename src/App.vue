<template>
  <div class="container">
    <header class="header">
      <h1 class="header__title">Регистрация</h1>
      <p class="header__subtitle">Уже есть аккаунт? <a href="#" class="header__subtitle-link">Войти</a></p>
    </header>
    <main>
      <signup-form />
    </main>
  </div>
</template>

<script>
import SignupForm from './components/SignupForm'
export default {
  name: 'App',
  components: {
    SignupForm
  }
}
</script>
