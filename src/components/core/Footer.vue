<template>
  <v-footer height="60" class="mt-5 justify-center text-xs-center d-block">
    <v-flex
      lighten2
      py-3
      text-xs-center
      white--text
      xs12
    >
      Copyright © 2019 Aurum Pacific (China) Group Limited. All rights reserved. Version: {{ appVersion }}
    </v-flex>
  </v-footer>
</template>

<script>
export default {
  name: 'Footer',
  computed: {
    appVersion() {
      return this.$store.getters.appVersion
    }
  }
}
</script>
