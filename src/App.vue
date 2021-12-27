<template>
  <div id="app">
    <section class="container">
      <header class="header">
        <h1 class="header__text">Conversor de moedas</h1>
      </header>
      <main class="cards">
        <Converter class="card" :from="'USD'" :to="'BRL'" />
        <Converter class="card" :from="'JPY'" :to="'BRL'" />
        <Converter class="card" :from="'BGN'" :to="'BRL'" />
        <Converter class="card" :from="'CZK'" :to="'BRL'" />
        <Converter class="card" :from="'DKK'" :to="'BRL'" />
      </main>
    </section>
  </div>
</template>

<script>
import Converter from "./components/Converter.vue";

export default {
  name: "App",
  components: { Converter },
};
</script>

<style>
body,
html {
  height: 100vh;
  width: 100vw;
}

* {
  font-family: "Poppins", sans-serif;
  box-sizing: content-box;
  margin: 0;
  padding: 0;
}

.container {
  padding: 15px;
}

.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.card {
  margin: 15px;
}

.header__text {
  font-weight: 400;
  text-align: center;
}
</style>
