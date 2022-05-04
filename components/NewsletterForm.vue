<template>
  <div class="newsletter-form-container">
    <div
      class="newsletter-form"
    >
      <div class="flex items-center space-x-2">
        <input
          id="email"
          v-model="form.email"
          type="email"
          name="email"
          class="w-full px-2 py-4 sm:py-3 rounded-lg sm:rounded-md text-sm focus:outline-none border border-[#AAAAAA] placeholder-[#888]"
          placeholder="Enter your email"
          aria-label="Email"
          aria-describedby="button-newsletter"
        >
        <button
          id="button-newsletter"
          class="bg-blue-gradient px-4 py-4 sm:py-3 rounded-md text-white hover:shadow-md transition duration-300"
          :class="{disabled: form.sending}"
          type="submit"
          @click.prevent="validateForm"
        >
        <ArrowRightIcon :size="20" />
        </button>
      </div>
      <transition name="status">
        <div
          v-if="form.errors.length"
          :class="form.success ? 'alert-success' : 'alert-danger'"
          class="alert"
          role="alert"
        >
          <ul>
            <li
              v-for="(error, index) in form.errors"
              :key="index"
            >
            {{ error }}
            </li>
          </ul>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'NewsletterForm',
  data() {
    return {
      form: {
        email: null,
        errors: [],
        validated: false,
        sending: false,
        success: false,
      },
    }
  },
  methods: {
    validateForm() {
      this.form.success = false;
      this.form.errors = [];
      if (!this.form.email) {
        this.form.errors.push('Email required.');
      } else if (!this.validEmail(this.form.email)) {
        this.form.errors.push('Valid email required.');
      }
      if (!this.form.errors.length) {
        this.subscribe();
        return true;
      } else {
        this.closeFormStatus();
      }
    },
    validEmail(email) {
      const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
    closeFormStatus() {
      setTimeout(()=> {
        this.form.errors = [];
      }, 3000);
    },
    resetFormEmail() {
      setTimeout(()=> {
        this.form.email = '';
      }, 3000);
    },
    async subscribe() {
      this.form.sending = true;
      this.form.errors.push('Sending...');
      try {
        const response = await axios.post('/api/subscribe', {email: this.form.email});
        this.form.success = true;
        this.resetFormEmail();
        this.form.errors.push(`Thank you: ${this.form.email} ${response.data}!`);
      } catch (error) {
        this.form.errors.push(`Error (${error.response.data.status}): ${error.response.data.title}`);
      } finally {
        this.closeFormStatus();
        this.form.sending = false;
      }
    }
  }
}
</script>

<style scoped>
  .newsletter-form-container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
  }
  .newsletter-form {
    max-width: 450px;
  }
  .newsletter-form__input-group {
    margin-bottom: 10px;
  }
  .status-enter {
    height: 0;
    opacity: 0;
  }
  .status-enter-to {
    transition: height 1s ease-in-out, opacity 1s ease-in-out;
    overflow: hidden;
  }
  ::-webkit-input-placeholder {
    color: #cecece;
  }
  ::-moz-placeholder {
    color: #cecece;
  }
  :-ms-input-placeholder {
    color: #cecece;
  }
  :-moz-placeholder {
    color: #cecece;
  }
</style>
