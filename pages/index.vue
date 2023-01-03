<template>
  <div>
    <NavBar/>
    <HomeCarousel :sale_items="sale_items"/>
    <TheFooter/>
  </div>
</template>

<script>
import NavBar from '~/components/NavBar.vue';
import TheFooter from '~/components/TheFooter.vue';
import HomeCarousel from '~/components/HomeCarousel.vue';

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

  components: { NavBar, TheFooter, HomeCarousel },
}
</script>
