<template>
  <div>
    <div id="nav">
      <router-link id="logo-url" to="/">
        <img id="logo" :src="logo" :alt="alt">
      </router-link>
      <router-link to="/">Fazer Pedido</router-link>
      <router-link to="/pedidos">Pedidos</router-link>
    </div>
  </div>
</template>

<script>

export default {
  name: "Navbar",
  props: ["logo", "alt"]
}
</script>

<style scoped>
  #nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  #logo-url {
    display: flex;
    align-items: center;
    text-decoration: none;
  }

  #logo {
    width: 40px;
    height: 40px;
    margin-right: 10px;
  }

  #nav a {
    color: #fcba03;
    text-decoration: none;
    margin: 0 10px;
    font-size: 18px;
    transition: color 0.3s;
  }

  #nav a:hover {
    color: #fff;
  }

  /* Estilo para menu responsivo */
  @media (max-width: 768px) {
    #nav {
      flex-direction: column;
      align-items: flex-start;
    }

    #logo-url {
      margin-bottom: 10px;
    }

    #nav a {
      display: block;
      margin: 8px 0;
    }
  }
</style>
