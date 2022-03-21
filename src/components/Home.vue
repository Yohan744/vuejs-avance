<template>

  <header>
    <h1>Fake store API</h1>
    <h1>cart</h1>
  </header>

  <div class="global-wrapper">

    <div v-for="item in items" v-bind:key="item.id" class="productWrapper" v-bind:class="[item.active?'activeItem activeButton':'']" @click="activeCart(item)">
      <div class="image">
        <img :src="item.image">
      </div>
      <div class="info">
        <h3>{{ item.title }}</h3>
        <p>{{ item.price }} €</p>
      </div>
      <button @click="addToCart(item)">Add to cart</button>
    </div>

  </div>

</template>

<script>

const axios = require('axios').default;

async function getStore() {
  try {
    const response = await axios.get('https://fakestoreapi.com/products');
    console.log(response);
    return response.data
  } catch (error) {
    console.error(error);
    return null
  }
}

getStore()

export default {
  name: 'HomeStore',

  data() {
    return {
      items: [],
      cart: []
    }

  },

  methods: {
    activeCart(item) {
      item.active = !item.active;
      this.items[item.id - 1].active = item.active
    },
    addToCart(item) {
      this.cart.push(item)
      console.log("===== CART =====")
      console.log(this.cart)
      console.log("================")
    }
  },

  created() {
    (async () => {
      const data = await getStore()
      for (let i = 0; i < data.length; i++) {
        this.items.push({id: data[i].id, title: data[i].title, image: data[i].image, price: data[i].price, active : false})
      }
    })()

  }

}

</script>

<style lang="scss">

* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  padding: 20px 40px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  background: #202020;
  color: white;
  z-index: 1;
}

.global-wrapper {
  position: relative;
  margin-top: 120px;
  padding: 0 50px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;

  .productWrapper {
    position: relative;
    margin: 50px;
    display: flex;
    flex-direction: column;
    border: 3px solid transparent;
    cursor: pointer;
    transition: 0.35s ease-in-out all;

    .image {
      position: relative;
      height: 225px;
      width: 225px;
      background: transparent;

      img {
        height: 100%;
        width: 100%;
        object-fit: contain;
      }

    }

    .info {
      position: relative;
      padding: 10px 0;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      font-family: Poppins, sans-serif;
      font-size: 14px;
      color: black;

      h3 {
        width: 110px;
        white-space: nowrap;
        overflow: hidden;
      }

    }

    button {
      position: relative;
      padding: 10px 0;
      font-family: Poppins, sans-serif;
      font-size: 16px;
      color: black;
      display: none;
      cursor: pointer;
      border: none;
    }

  }

}

.activeItem {
  border: 3px solid dodgerblue !important;
  transition: 0.35s ease-in-out all;
}

.activeButton button {
  display: block !important;
}

</style>
