<template>
  <div class="home">
    <!-- Hero Section -->
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">Welcome to Ecommerce</p>
        <p class="subtitle">The best ecommerce platform</p>
      </div>
    </section>

    <!-- Latest Products Section -->
    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest products</h2>
      </div>

      <!-- Product Card -->
      <product-box
      v-for="product in latestproducts"
      v-bind:key="product.id"
      v-bind:product="product"/>
    </div>
  </div>
</template>


<script>
import axios from 'axios'
import ProductBox from '@/components/ProductBox'

export default {
  name: 'Home',
  data(){
    return{
      latestproducts:[]
    }
  },
  components: {
    ProductBox
  },
  mounted(){
    this.getLatestProducts()

    document.title = 'Home | Ecom'

  },
  methods:{
    async getLatestProducts(){
      this.$store.commit('setIsLoading', true)

      await axios
      .get('api/v1/latest-products/')
      .then(response =>{
        this.latestproducts = response.data
      })
      .catch(error =>{
        console.log(error)
      })
      this.$store.commit('setIsLoading', false)

    }
  }
}
</script>

<!-- <style scoped>
  .image{
    margin-top: -1.25rem;
    margin-left: -1.25rem;
    margin-right: -1.25rem;
  }
</style> -->