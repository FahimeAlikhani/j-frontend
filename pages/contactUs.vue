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
        <label for="full_name" class="sr-only">Full name*</label>
        <div class="relative rounded-md shadow-sm">
          <input
            id="full_name"
            v-model="name"
            required
            name="name"
            class="form-input block w-full py-3 px-4 placeholder-gray-500 transition ease-in-out duration-150"
            placeholder="Full name*"
          />
        </div>
      </div>
      <div>
        <label for="email" class="sr-only">Email*</label>
        <div class="relative rounded-md shadow-sm">
          <input
            id="email"
            v-model="email"
            name="email"
            required
            type="email"
            class="form-input block w-full py-3 px-4 placeholder-gray-500 transition ease-in-out duration-150"
            placeholder="Email*"
          />
        </div>
      </div>
      <div>
        <label for="phone" class="sr-only">Phone</label>
        <div class="relative rounded-md shadow-sm">
          <input
            id="phone"
            v-model="phone"
            name="phone"
            class="form-input block w-full py-3 px-4 placeholder-gray-500 transition ease-in-out duration-150"
            placeholder="Phone"
          />
        </div>
      </div>
      <div>
        <label for="message" class="sr-only">Message</label>
        <div class="relative rounded-md shadow-sm">
          <textarea
            id="message"
            v-model="message"
            name="message"
            required
            rows="4"
            class="form-input block w-full py-3 px-4 placeholder-gray-500 transition ease-in-out duration-150"
            placeholder="Message*"
          ></textarea>
        </div>
      </div>
      <div class="">
        <button
            type="submit"
             class="button max-w-full px-8 py-4 bg-gradient-to-r from-[#468ef9] to-[#0c66ee] border border-[#0c66ee] text-white "
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
