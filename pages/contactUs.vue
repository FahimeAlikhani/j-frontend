<template>
<section class="section">
  <SectionPage>
  <div>
   <!-- This shows a success message if the form was submitted correctly. -->
    <div v-if="success" class="rounded bg-indigo-500 text-white text-lg p-4">
      Great! Your message has been sent successfully. I will try to respond
      quickly.
    </div>
    <form
      v-else
      class="grid grid-cols-1 gap-y-6"
      @:submit.prevent="sendMessage"

    >
      <!-- Here an error is displayed if something goes wrong -->
      <div v-if="errored" class="rounded bg-red-200 text-lg p-4">
        Bummer, Something went wrong. Did you fill out all of the fields?
      </div>
      <div>
          <input
            id="full_name"
            v-model="name"
            required
            type="text"
            name="name"
            class="flex space-x-10 py-3 px-3 w-80 rounded-lg"
            placeholder="Full name*"
          />
      </div>
      <div>
          <input
            id="email"
            v-model="email"
            required
            type="email"
            name="email"
            class="flex space-x-10 py-3 px-3 w-80 rounded-lg"
            placeholder="Email*"
          />
      </div>
      <div>
          <input
            id="phone"
            v-model="phone"
            type="text"
            name="phone"
            class="flex space-x-10 py-3 px-3 w-80 rounded-lg"
            placeholder="Phone"
          />
      </div>
      <div>
          <textarea
            id="message"
            v-model="message"
            required
            type="text"
            name="message"
            rows="4"
            class="flex space-x-10 py-3 px-3 w-80 rounded-lg "
            placeholder="Message*"
          ></textarea>
      </div>
      <div class="">
        <button
            type="submit"
             class="button max-w-full px-8 py-4 bg-gradient-to-r from-[#468ef9] to-[#0c66ee] border border-[#0c66ee] text-white rounded-lg"
          >
            {{ loading ? "Sending Message..." : "Submit" }}
         </button>
      </div>
    </form>
  </div>
  </SectionPage>
</section>
</template>
<script>
import SectionPage from '../components/base/Sectionn.vue'

export default {
  name:'AboutUs',
  components: {
    SectionPage,
  },
  data() {
    return {
      loading: false,
      success: false,
      errored: false,
      name: "",
      email: "",
      phone: "",
      message: "",
    }
  },
  methods: {
    sendMessage() {
      this.loading = true;
      this.$axios
        .post("/messages", {
          name: this.name,
          email: this.email,
          phone: this.phone,
          message: this.message,
        }).then(response => {
          this.success = true
          this.errored =false
        })
        .catch(() => {
          this.errored = true
        })
        .finally(() => {
          this.loading = false
        });
    },
  }
}
</script>
<style scoped>
.section {
  margin-top: 24px;
  margin-bottom: 24px;
}
</style>
