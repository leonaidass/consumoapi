<template>
  <v-app id="app">
   <v-app-bar app color="green">
      <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/admin">Administrador</router-link>
    </div>

   </v-app-bar>
     <v-main>
       <router-view/>
     </v-main>
  </v-app>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #e1e6ec;

    &.router-link-exact-active {
      color: #fcfcfc;
    }
  }
}
</style>
