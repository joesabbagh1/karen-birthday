<template>
  <v-container>
    <v-row>
      <Opening />
    </v-row>
    <v-row>
      <Options />
    </v-row>
  </v-container>
</template>

<script>
import Opening from '../components/Opening.vue'
import Options from '../components/Options.vue'

  export default {
    name: 'Home',

    components: {
        Opening,
        Options
    },
  }
</script>
