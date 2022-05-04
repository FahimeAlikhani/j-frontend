<template>
  <div class="notification is-danger">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: 'NotificationComponent',
  // eslint-disable-next-line vue/require-prop-types
  props: ['message']
}
</script>
