<template>
  <header>
    <router-link to="/">
      <h1><span>Movie</span> App</h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
  <footer>
    <p style="width: 100%;">
      <MARQUEE bgColor="" height="auto" scrollamount="15" style="color: white; font-size: 15px; line-height: 30px; text-align: center;">
        COPYRIGHT 2020. 박경준. All rights reserved.
      </MARQUEE>
    </p>
  </footer>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
  
  &::selection {
    background: transparentize($color: #42B883, $amount: 0.5)
  }
  
  #app {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  
  body {
    background-color: #35495E;
  }
  
  footer {
    margin-top: 70px;
  }
  
  main {
    flex: 1;
  }
  
  a {
    text-decoration: none;
  }
  
  header {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 10px 16px;
    background-color: #2C3D4E;
    box-shadow: 0 0 6px rgba(0, 0, 0, 0.1);
  
    h1 {
      color : #fff;
      font-size: 28px;
      
      span {
        color: #42B883;
      }
    }
  }
}  
</style>
