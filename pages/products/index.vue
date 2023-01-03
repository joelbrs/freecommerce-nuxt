<template>
  <div>
    <NavBar/>

    <v-container>
      <v-row dense>
        <v-col md="3">
          <div>
            <v-text-field prepend-inner-icon="mdi-magnify" outlined clearable placeholder="Search" v-model="search"></v-text-field>
            <v-list subheader color="transparent" v-if="$vuetify.breakpoint.mdAndUp">
              <v-subheader>Categories</v-subheader>
              <v-list-item v-for="(category, i) in categories" :key="`category${i}`" link>
                <v-list-item-avatar>
                  <v-img :src="category.image"></v-img>
                </v-list-item-avatar>

                <v-list-item-content>
                  <v-list-title>
                    {{ category.name }}
                  </v-list-title>
                </v-list-item-content>
              </v-list-item>


            </v-list>
          </div>
        </v-col>

        <v-col md="9">
          <v-row>
            <template v-for="(product, i) in filteredProducts" >
              <v-col cols="12" md="6" :key="`product${product.id}-${i}`">
                <v-card link color="surface" class="el ma-2 mb-5 mr-5">
                  <v-img :src="product.image" height="300">
                    <template #placeholder>
                      <v-row
                        class="fill-height"
                        justify="center"
                        align="center"
                      >
                        <v-progress-circular
                          width="2"
                          size="100"
                          color="primary"
                          indeterminate
                        >
                        </v-progress-circular>
                      </v-row>
                    </template>
                  </v-img>

                  <v-card-title class="text-md-body-1 font-weight-bold">
                    {{ product.name }}
                  </v-card-title>
                  <v-card-subtitle class="primary--text pb-3">
                    {{ product.price }}
                  </v-card-subtitle>

                  <v-card-text>
                    <v-chip
                      x-small
                      label
                      outlined
                      class="mr-1"
                      v-for="(tag, i) in product.tags"
                      :key="`prod${product.id}-${i}`"
                    >
                      {{ tag }}
                    </v-chip>
                  </v-card-text>
                </v-card>
              </v-col>
            </template>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
    <TheFooter/>
    <ScrollTop/>
  </div>
</template>

<script>
import NavBar from '~/components/NavBar.vue'
import TheFooter from '~/components/TheFooter.vue'
import ScrollTop from '~/components/ScrollTop.vue'

export default {
  data() {
    return {
      products: null,
      categories: null,
      search: null
    }
  },

  computed: {
    filteredProducts() {
      if (!this.search || !this.products) {
        return this.products || []
      }

      return this.products.filter(p => {
        const s = this.search.toLowerCase()
        const n = p.name.toLowerCase()
        const price = p.price.toString()
        const sparice = p.salePrice?.toString() || ''
        const r = p.ratings.toString()

        return n.includes(s) || price.includes(s) || sparice.includes(s) || r.includes(s)
      })
    }
  },

  async created() {
    this.products = await this.$content('products').where({onSale: true}).fetch()
    this.categories = await this.$content('category').fetch()
  },

  components: { NavBar, TheFooter, ScrollTop }
}
</script>

<style>

</style>
