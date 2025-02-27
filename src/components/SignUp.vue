<template>
  <v-container fluid>
    <v-layout row wrap>
      <Heading :title="$t('signup.TITLE')" />
      <v-flex xs12 sm6 offset-sm3>
        <form @submit.prevent="submit">
          <v-layout column>
            <v-flex>
              <v-text-field
                id="name"
                v-model="name"
                v-validate.disable="'required'"
                name="name"
                :label="$t('signup.NAME')"
                :data-vv-as="$t('signup.NAME')"
                :error="errors.has('name')"
                :error-messages="errors.collect('name')"
                autocomplete="off"
              />
            </v-flex>
            <v-flex>
              <v-text-field
                id="email"
                v-model="email"
                v-validate.disable="'required|email'"
                name="email"
                type="email"
                :label="$t('signup.EMAIL')"
                :data-vv-as="$t('signup.EMAIL')"
                :error="errors.has('email')"
                :error-messages="errors.collect('email')"
                autocomplete="off"
              />
            </v-flex>
            <v-flex>
              <v-text-field
                id="password"
                ref="password"
                v-model="password"
                v-validate.disable="'required|min:5'"
                name="password"
                type="password"
                :label="$t('signup.PASSWORD')"
                :data-vv-as="$t('signup.PASSWORD')"
                :error="errors.has('password')"
                :error-messages="errors.collect('password')"
                autocomplete="off"
              />
            </v-flex>
            <v-flex>
              <v-text-field
                id="confirmPassword"
                v-model="confirmPassword"
                v-validate.disable="'required|min:5|confirmed:password'"
                name="confirmPassword"
                type="password"
                :label="$t('signup.CONFIRM_PASSWORD')"
                :data-vv-as="$t('signup.PASSWORD')"
                :error="errors.has('confirmPassword')"
                :error-messages="errors.collect('confirmPassword')"
                autocomplete="off"
              />
            </v-flex>
            <v-flex text-xs-center mt-5>
              <SubmitButton :text="$t('signup.SIGN_ME_UP')" />
            </v-flex>
          </v-layout>
        </form>
      </v-flex>
      <ErrorMessage />
    </v-layout>
  </v-container>
</template>

<script>
import router from '@/router'
import { mapActions } from 'vuex'

export default {
  metaInfo() {
    return {
      title: this.$store.getters.appTitle,
      titleTemplate: `${this.$t('signup.TITLE')} - %s`
    }
  },
  data() {
    return {
      name: '',
      email: '',
      password: '',
      confirmPassword: ''
    }
  },
  methods: {
    ...mapActions(['userSignUp']),
    async submit() {
      const valid = await this.$validator.validateAll()
      if (valid) {
        await this.userSignUp({
          name: this.name,
          email: this.email,
          password: this.password
        })
      }
    }
  },
  created() {
    if (this.$store.state.auth.isTokenSet) {
      router.push({ name: 'home' })
    }
  }
}
</script>
