<template>
  <nav id="navbar" class="relative z-10 w-full text-neutral-800">
    <div class="flex flex-col max-w-screen-xl px-8 mx-auto lg:items-center lg:justify-between lg:flex-row py-4">
      <div class="flex flex-col lg:flex-row items-center space-x-4 xl:space-x-8">
        <div class="w-full flex flex-row items-center justify-between py-6">
          <div>
            <img :src="require('~/assets/img/logo/Logojade.svg')" class="w-24 xl:w-28" alt="Jadee Logo" />
          </div>
          <button class="rounded-lg lg:hidden focus:outline-none focus:shadow-outline" @click="open = !open">
            <SegmentIcon v-if="!open" :size="24" />
            <CloseIcon v-else :size="24" />
          </button>
        </div>
        <ul
          :class="[open ? 'flex' : 'hidden lg:flex']"
          class=" w-full h-auto flex flex-col flex-grow font-bold text-4xl lg:items-center pb-4 lg:pb-0 lg:justify-end lg:flex-row origin-top duration-300 xl:space-x-6 space-y-3 lg:space-y-0"
        >
          <NavLink name="Home" url="/" />
          <NavLink name="AboutUs" url="/aboutUs" />
          <NavLink name="ContactUs" url="/contactUs" />
        </ul>
      </div>
      <div :class="[open ? 'flex' : 'hidden lg:flex']" class="space-x-3">
        <base-button  class="px-8 xl:px-10 py-3 mt-2 bg-inherit text-gradient border border-[#0c66ee]" >

          <nuxt-link class="navbar-item" to="/login">Login</nuxt-link>
        </base-button>
        <base-button class="px-8 xl:px-10 py-3 mt-2 bg-gradient-to-r from-[#468ef9] to-[#0c66ee] text-white">

          <nuxt-link class="navbar-item" to="/register">Sign Up</nuxt-link>
        </base-button>
      </div>
    </div>
  </nav>
</template>
<script>
export default {
  name: 'BaseNavbar',
  data() {
    return {
      open: false,
      dropdownNavbar: false,
    }
  },
}
</script>
