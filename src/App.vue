<template>
  <router-view />
  <div class="footer-fixed text-white text-center pt-1 border-top">
    <div class="row rowIcons">
      <div class="col-3">
        <router-link to="/listCheck"><i class="bi bi-list-check"></i></router-link>
      </div>
      <div class="col-3">
        <router-link to="/search"><i class="bi bi-search"></i></router-link>
      </div>
      <div class="col-3">
        <router-link to="/fav"><i class="bi bi-heart"></i></router-link>
      </div>
      <div class="col-3">
        <router-link to="/profile"><i class="bi bi-person"></i></router-link>
      </div>
    </div>
  </div>
</template>

<style>
* {
  background: black;
}

.rowIcons a{
  font-size: 1.6rem;
  color: white;
}

.footer-fixed {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  z-index: 1030;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #ffff;
}

.fs-7{
  font-size: 0.8rem;
}
</style>
