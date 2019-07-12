<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li class="nav-item">
            <img class="logo" src="./assets/logo.png" width="32" height="32" alt="logo">
            Build Here!
          </li>
        </ul>
      </nav>
    </header>
    <main>
    <RobotBuilder/>
    </main>
  </div>
</template>
<!-- Start from 22, 21- check the end lesson-->
<script>
// import HomePage from './home/HomePage.vue';
import RobotBuilder from './build/RobotBuilder.vue';

export default {
  name: 'app',
  components: {
    RobotBuilder,
  },
};
</script>

<style>
body{
  background: linear-gradient(to bottom , #555, #999);
  background-attachment: fixed;
}

</style>


<style scoped>


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}
main {
  margin: 0 auto;
  background-color: #fff;
  width: 1024px;
  min-height: 300px;
  padding: 30px;
}


header {
  background-color: #999;
  width: 1084px;
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
  border-right: 1px solid #bbb;
  cursor: pointer;
}
.nav-item:hover {
  background: #fff;
  transition: 1s
}
.logo {
  vertical-align: middle;
  height: 30px;
}
</style>
