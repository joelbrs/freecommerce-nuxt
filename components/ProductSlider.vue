<template>
  <v-slide-group>
    <v-slide-item v-for="(product, i) in products" :key="`hotProduct=${i}`">
      <v-card link colo="surface" width="300" class="el ma-2 mb-5 mr-5">
        <v-img height="300" :src="product.image">
          <template #placeholder>
            <v-row class="fill-height" justify="center" align="center">
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
          <v-chip x-small label outlined class="mr-1" v-for="(tag, i) in product.tags"  :key="`prod${product.id}-${i}`">
            {{ tag }}
          </v-chip>
        </v-card-text>
      </v-card>
    </v-slide-item>
  </v-slide-group>
</template>

<script>
export default {
  name: 'ProductSlider',

  props: {
    products: Array
  }
}
</script>

<style>

</style>
