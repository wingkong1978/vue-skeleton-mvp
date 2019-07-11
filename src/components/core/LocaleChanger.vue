<template>
  <v-menu v-model="showMenu" offset-y>
    <v-btn slot="activator" class="btnLocaleActivation" flat>
      <v-icon>mdi-earth</v-icon>
      &nbsp;{{ displayLocale }}
    </v-btn>
    <v-list>
      <v-list-tile
        v-for="(item, i) in langs"
        :key="`Lang${i}`"
        active-class="white--text"
        :value="item.lang"
        :class="[item.class]"
        @click="switchLocale(item.lang)"
      >
        <country-flag :country="item.flag" size="small" class="pl-5" />
        <v-list-tile-title class="ml-3">{{
          item.lang.toUpperCase()
        }}</v-list-tile-title>
      </v-list-tile>
    </v-list>
  </v-menu>
</template>

<script>
import CountryFlag from 'vue-country-flag'

export default {
  components: {
    CountryFlag
  },
  data() {
    return {
      showMenu: false,
      langs: [
        {
          lang: 'en',
          flag: 'gb',
          class: 'btnEN'
        },
        {
          lang: 'es',
          flag: 'es',
          class: 'btnES'
        }
      ]
    }
  },
  computed: {
    displayLocale() {
      return this.$i18n.locale
    }
  },
  methods: {
    switchLocale(lang) {
      this.$store.dispatch('setLocale', lang)
    }
  }
}
</script>
