<template>
  <div>
    <v-app-bar
      color="surface"
      height="80"
      class="el"
      :style="{ padding: $vuetify.breakpoint.smAndUp ? '0px 100px' : '' }"
    >
      <v-toolbar-title @click="$router.push('/')" class="text-md-h5 font-weight-bold pointer">
        FreeCommerce
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn nuxt to="/products" icon>
        <v-icon size="20">mdi-store-outline</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon size="20">mdi-cart-outline</v-icon>
      </v-btn>

      <v-divider vertical class="mx-md-5 mx-2"></v-divider>

      <v-btn icon>
        <v-icon size="20">mdi-brightness-7</v-icon>
      </v-btn>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  name: 'NavBar'
}
</script>

<style>

</style>
