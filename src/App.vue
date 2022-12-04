<template>
  <v-app>
    <v-main>
      <div class="container-main">
        <CompCalculadora/>
        <CompInfo/>
      </div>
    </v-main>
  </v-app>
</template>

<script>
import CompCalculadora from './components/CompCalculadora.vue';
import CompInfo from './components/CompInfo.vue';

export default {
  name: 'App',

  components: {
    CompCalculadora,
    CompInfo
  },

  data: () => ({
    //
  }),
};
</script>

<style>
div.v-application--wrap {
  background-color: #266ABC;
}

main {
  margin: 1rem 0;
}

.container-main {
  background-color: #EFEFEF;
  padding: 2rem;
  border-radius: 25px;
  width: 80%;
  margin: auto;
}
</style>