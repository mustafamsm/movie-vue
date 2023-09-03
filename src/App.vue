<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>
  <header>

    <RouterLink to="/">
      <h1><span>Vue</span>Movies</h1>
    </RouterLink>


  </header>
  <main>
    
    <RouterView />
  </main>
</template>

<style lang="scss"  >
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
&::selection{
  background: transparentize($color: #428883, $amount: 0.5);
}

}

body {
  background-color: #35495E;

}

a {
  text-decoration: none;

}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #2c3D4E;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
}

h1 {
  color: white;
  font-size: 1.5rem;

  span {
    color: #41B883;
  }
}
</style>
