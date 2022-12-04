<template>
  <v-app>
    <v-main>
      <CompCalculadora/>
    </v-main>
    <!-- <v-main>
      <HelloWorld/>
    </v-main> -->
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import CompCalculadora from './components/CompCalculadora.vue';

export default {
  name: 'App',

  components: {
    // HelloWorld,
    CompCalculadora
  },

  data: () => ({
    //
  }),
};
</script>
