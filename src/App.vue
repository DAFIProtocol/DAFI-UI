<template>
  <div id="app">
    <span class="d-flex justify-content-center">
      <a href="/">
      <img src="./assets/logo.png" alt="">
      </a>
    </span>
    <router-view/>

  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
    @media only screen and (max-width: 769px) {
        #footer{
            height: 60px;
            width: 90vw!important;
            border-top-left-radius: 5px;
            border-top-right-radius: 5px;
            margin: auto;
            background: #262625;
            display: flex;
            justify-content: space-around;
            position: fixed;
            top: 93%;
            left: 20px!important;
        }
    }

    #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-height: 100vh;
  background: linear-gradient(rgba(34, 34, 34, 1), rgba(17, 17, 17, 1));
}
  img {
    height: 160px;
    width: 160px;
    margin-bottom: 30px;
  }
    #footer{

        height: 60px;
        width: 25vw;
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
        margin: auto;
        background: #262625;
        display: flex;
        justify-content: space-around;
        position: fixed;
        top: 93%;
        left: 38vw;

    }
    .circ{
        background: #0292c6;
        padding: 15px;
        width: 66px;
        height: 66px;
        border-radius: 50%;
        color: #eee;
        position: relative;
        top: -24px;
    }
    .ic{
        margin-top: 6px;
        color: #eee;
        text-align: center;
        font-size: 36px;
    }
</style>
