<template>
  <div id="app">
    <!--
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    -->
    <TopNav>

    </TopNav>
    <main>
      <Home/>
    </main>
  </div>
</template>

<script>
import Home from "./modules/home/Home.vue";
import TopNav from "./components/topnav/TopNav";

export default {
  name: 'App',
  components: {
    Home,
    TopNav
  }
}
</script>

