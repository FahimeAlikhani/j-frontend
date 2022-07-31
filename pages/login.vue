<template>
  <section class="section">
    <SectionPage>
    <div class="container">
      <div class="columns">
        <div class="column is-2 is-offset-2">
          <h2 class="title has-text-centered">Welcome back!</h2>

          <Notification v-if="error" :message="error" />

          <form method="post" @submit.prevent="login">
            <div class="field">
              <label class="label">Email</label>
              <div class="control">
                <input
                  v-model="email"
                  type="email"
                  class="input rounded-lg"
                  name="email"

                />
              </div>
            </div>
            <div class="field">
              <label class="label">Password</label>
              <div class="control">
                <input
                  v-model="password"
                  type="password"
                  class="input rounded-lg"
                  name="password"

                />
              </div>
            </div>
            <div class="control"> 
              <button type="submit" class="button is-dark is-fullwidth">Log In</button>
            </div>
          </form>
          <div
            class="has-text-centered"
            style="margin-top: 20px">
            <p class="label">
              Don't have an account? <nuxt-link class="button" to="/register">Register</nuxt-link>
            </p>
          </div>
        </div>
      </div>
    </div>
    </SectionPage>
  </section>
</template>

<script>
import SectionPage from '../components/base/Sectionn.vue'
import Notification from '~/components/Notification'

export default {
  name:'LoginPage',
  components: {
    Notification,
    SectionPage,
  },

  data() {
    return {
      email: '',
      password: '',
      error: null
    }
  },

  methods: {
    async login() {
      try {
        await this.$auth.loginWith('local', {
          data: {
          email: this.email,
          password: this.password
          }
        })

        this.$router.push('/')
      } catch (e) {
        this.error = e.response.data.message
      }
    }
  }
}
</script>
<style scoped>
.button {
  background: rgb(57, 132, 244);
  background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-top: 20px;
}
.has-text-centered {
  margin-bottom: 24px;
}
.section {
  margin-top: 24px;
  margin-bottom: 24px;
}
</style>
