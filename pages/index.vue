<template>
  <div>
    <NavBar/>
    <HomeCarousel :sale_items="sale_items"/>
    <br><br>

    <v-container>
      <h1 class="text-md-h4 text-h6">
        Check these out
      </h1>
      <br>

      <ProductSlider :products="products"/>
      <br><br><br>
      <NewsLetter/>
    </v-container>
    <TheFooter/>

    <ScrollTop/>
  </div>
</template>

<script>
import NavBar from '~/components/NavBar.vue';
import TheFooter from '~/components/TheFooter.vue';
import HomeCarousel from '~/components/HomeCarousel.vue';
import ProductSlider from '~/components/ProductSlider.vue';
import NewsLetter from '~/components/NewsLetter.vue';
import ScrollTop from '~/components/ScrollTop.vue'

export default {
  name: 'IndexPage',

  data() {
    return {
      products: null,
      sale_items: null
    }
  },

  async created() {
    this.sale_items = await this.$content('products').where({onSale: true}).fetch()
    this.products = await this.$content('products').fetch()
  },

  components: { NavBar, TheFooter, HomeCarousel, ProductSlider, NewsLetter, ScrollTop },
}
</script>
