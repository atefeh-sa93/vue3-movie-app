<template>
  <header>
    <router-link :to="{name: 'home'}">
      <h1>
        <span>Vue</span>
        Movies
      </h1>
    </router-link>
  </header>
  <main>
    <router-view/>
  </main>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  font-family: 'Fira Sans', sans-serif;
  box-sizing: border-box;

  &::selection {
    background: transparentize(#42B883, .5)
  }
}
body {
  background: #35495e;
}
 a {
   text-decoration: none;
 }
 header {
   display: flex;
    align-items: center;
    justify-content: center;
    padding: 10px 16px;
    background: #2c3d4e;
    box-shadow: 0px 0px 6px rgba(0,0,0,0.1);
 }
  h1 {
    color: #fff;
    font-size: 28px;
    
    span {
      color: #42B883;
    }
  }
</style>
