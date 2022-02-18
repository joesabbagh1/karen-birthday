<template>
  <v-container>
    <v-row>
      <Options />
    </v-row>
  </v-container>
</template>

<script>
import Options from '../components/Options.vue'

  export default {
    name: 'Home',

    components: {
        Options
    },
  }
</script>
