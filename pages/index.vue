<template>
  <div>
    <header-div />
    <main>
      <product-form/>
      <transition-group class="products" name="products-list" tag="div">
        <product-card class="products-list-item" v-for="product in products" :key="product.productKey" :product="product" />
      </transition-group>
    </main>
  </div>
</template>

<script>
import ProductCard from '../components/ProductCard.vue'
export default {
  name: 'IndexPage',
  components: { ProductCard },
  data () {
    return {
      sortMode: 'По умолчанию',
      defaultProducts: [
        { productKey: 0, productName: 'Наименование товара', productDescription: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', imageLink: 'https://patentsorgu.com/public/depo/dosyalar/3_2.jpg', productPrice: 10000 },
        { productKey: 1, productName: 'Наименование товара', productDescription: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', imageLink: 'https://patentsorgu.com/public/depo/dosyalar/3_2.jpg', productPrice: 10000 },
        { productKey: 2, productName: 'Наименование товара', productDescription: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', imageLink: 'https://patentsorgu.com/public/depo/dosyalar/3_2.jpg', productPrice: 10000 },
        { productKey: 3, productName: 'Наименование товара', productDescription: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', imageLink: 'https://patentsorgu.com/public/depo/dosyalar/3_2.jpg', productPrice: 10000 }
      ],
      products: []
    }
  },
  mounted () {
    if (localStorage.getItem('products') !== null) {
      this.products = JSON.parse(localStorage.products)
      console.log(1)
    } else {
      this.products = this.defaultProducts
      localStorage.products = JSON.stringify(this.defaultProducts)
      console.log(2)
    }
  },
  methods: {
    removeProduct (key) {
      this.products = this.products.filter(obj => obj.productKey !== key)
      this.updateLocaleStorage()
    },
    addProduct (name, description, link, price) {
      const currentDate = new Date()
      const timestamp = currentDate.getTime()
      this.products.push({ productKey: timestamp, productName: name, productDescription: description, imageLink: link, productPrice: price })
      this.updateLocaleStorage()
      this.sortProducts(this.sortMode)
    },
    updateLocaleStorage () {
      localStorage.products = JSON.stringify(this.products)
    },
    sortProducts (mode) {
      if (mode === 'По умолчанию') {
        this.products.sort((a, b) => +a.productKey - +b.productKey)
      } else if (mode === 'По цене min') {
        this.products.sort((a, b) => +a.productPrice - +b.productPrice)
      } else if (mode === 'По цене max') {
        this.products.sort((a, b) => +b.productPrice - +a.productPrice)
      } else if (mode === 'По наименованию') {
        this.products.sort((a, b) => (a.productName > b.productName) ? 1 : -1)
      }
      this.sortMode = mode
    }
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@300;400;600&display=swap');
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body{
    font-family: 'Source Sans Pro', sans-serif;
    padding: 1.969375rem;
    background: rgba(255, 254, 251, 0.8);
  }
  main{
    margin-top: 1rem;
    display: grid;
    grid-template-columns: 332px 1fr;
    gap: 1rem;
    @media (max-width: 743px){
      grid-template-columns: 1fr;
    }
    .products{
      display: grid;
      gap: 1rem;
      grid-template-columns: repeat(auto-fit, minmax(332px, 1fr));
      @media (max-width: 1090px){
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      }
    }
  }
  .products-list-item {
    transition: all 1s ease-in-out;
  }
  .products-list-enter,
  .products-list-leave-to {
    transform: translateX(-50px) !important;
    opacity: 0;
  }
  .products-list-leave-active {
    position: absolute;
    transform: translateX(-30px);
  }
</style>
