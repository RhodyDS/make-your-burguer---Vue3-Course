<template>
  <div id="main-banner">
    <h1>Make Your Burger</h1>
  </div>
</template>

<script>
  export default {
    name: "Banner"
  }
</script>

<style scoped>
  #main-banner {
    background-image: url('/img/burger.jpg');
    background-position: center;
    background-size: cover;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
  }

  #main-banner::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.6);
  }

  #main-banner h1 {
    color: #fcba03;
    text-align: center;
    font-size: 60px;
    padding: 20px 40px;
    z-index: 1;
  }

  @media (max-width: 768px) {
    #main-banner h1 {
      font-size: 40px;
      padding: 10px 20px;
    }
  }
</style>
