<template>
  <footer class="max-w-screen-xl px-8 mx-auto">
    <div class="w-full border-y border-[#DDDDDD]">
      <div class="w-full flex flex-wrap space-y-6">
        <div
          class="w-full sm:w-1/2 xl:w-fit flex flex-col sm:flex-row sm:px-6 py-6 sm:py-12 sm:space-x-10 sm:border-r border-[#DDDDDD]"
        >
          <div class="sm:hidden xl:block mb-6 sm:mb-0">
            <a href="#">
              <img :src="require('~/assets/img/logo/Logojade.svg')" class="w-24 -mt-2" alt="Nefa Logo" />
            </a>
          </div>
          <ul class="space-y-4">
            <NavLink name="AboutUs" url="#" />
            <NavLink name="ContactUs" url="#" />
          </ul>
        </div>

        <div
          class="sm:px-10 py-6 sm:py-12 w-full sm:w-1/2 xl:w-[22rem] space-y-4 border-t sm:border-t-0 border-[#DDDDDD]"
        >
          <h5 class="text-sm font-medium text-[#666666] focus:outline-none focus:shadow-outline">Newsletter</h5>
          <p class="text-sm text-[#666666] focus:outline-none focus:shadow-outline">
            Never miss anything crypto when <br class="sm:hidden" />you're on the go
          </p>
          <div class="flex items-center ">
            <NewsletterForm />

          </div>
        </div>
      </div>
    </div>
    <div class="py-8 sm:py-4 text-center text-sm text-[#666666] hover:text-gray-900">
      &copy; jade 2022
    </div>
  </footer>
</template>
<script>

import NewsletterForm from '@/components/NewsletterForm'
export default {
  name: 'BaseFooter',
  components: {
    NewsletterForm,
  },
}
</script>
