<template>
  <v-app>
    <v-main>
      <CompCalculadora/>
      <CompInfo/>
    </v-main>
    <!-- <v-main>
      <HelloWorld/>
    </v-main> -->
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import CompCalculadora from './components/CompCalculadora.vue';
import CompInfo from './components/CompInfo.vue';

export default {
  name: 'App',

  components: {
    // HelloWorld,
    CompCalculadora,
    CompInfo
  },

  data: () => ({
    //
  }),
};
</script>
