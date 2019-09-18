<template>
  <div id="app">
    <Header />
    <router-view/>
  </div>
</template>

<script>
import Header from './components/layout/Header';
export default {
  name: 'App',
  components: {
    Header
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  html {
    font-size: 62.5%;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    border: none;
    background-color: #555;
    color: #fff;
    padding: 0.7rem 2rem;
    cursor: pointer;
  }
  .btn:hover {
    background-color: #666;
  }
</style>
