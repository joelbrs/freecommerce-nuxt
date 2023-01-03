<template>
  <div>
    <NavBar/>
    <TheFooter/>
  </div>
</template>

<script>
import NavBar from '~/components/NavBar.vue';
import TheFooter from '~/components/TheFooter.vue';

export default {
  name: 'IndexPage',

  components: { NavBar, TheFooter }
}
</script>
