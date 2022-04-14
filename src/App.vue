<script setup>
import TheHeader from "./components/TheHeader.vue";
import RutGenerator from "./components/RutGenerator.vue";
import EmailGenerator from "./components/EmailGenerator.vue";
</script>

<template>
  <header>
    <img
      alt="RUT Random logo"
      class="logo"
      src="./assets/identity.png"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <TheHeader msg="RUT Random" />
      <RutGenerator />
    </div>
  </header>
  <header>
    <img
      alt="Correo Random logo"
      class="logo"
      src="./assets/email.png"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <TheHeader msg="Correo Random" />
      <EmailGenerator />
    </div>
  </header>
</template>

<style>
@import "./assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
    margin-bottom: 3rem;
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
