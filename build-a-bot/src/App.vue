<template>
  <header>
    <nav>
      <ul>
        <li>
          <img class="logo" src="../_course-resources/assets/build-a-bot-logo.png" alt="logo"/>
          Build-a-Bot
        </li>
      </ul>
    </nav>
  </header>
  <main>
    <!--<HomePage msg="Welcome to Your Vue.js App"/> -->
    <RobotBuilder/>
  </main>
</template>

<script>
// import HomePage from './home/HomePage.vue';
import RobotBuilder from './build/RobotBuilder.vue';
// import ProductSearch from './search/ProductSearch.vue';

export default {
  name: 'App',
  components: {
    RobotBuilder,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

body {
  background: linear-gradient(to bottom, #555, #999);
  background-attachment: fixed;
}
</style>

<style scoped>
main {
  margin: 0 auto;
  padding: 30px;
  background-color: white;
  width: 1400px;
  min-height: 300px;
}

header {
  background-color: #999;
  width: 1460px;
  margin: 0 auto;
}

ul {
  padding: 3px;
  display: flex;
}

.nav-item {
  display: inline-block;
  padding: 5px 10px;
  font-size: 22px;
  border-right: 1x solid #bbb;
}

.logo {
  vertical-align: middle;
  height: 30px;
}

</style>
