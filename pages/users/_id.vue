<template>
  <div class="flex flex-col items-center">
    <nuxt-link class="p-4 bg-purple-700 rounded-md" :to="{ name: 'index' }">
      Go back
    </nuxt-link>

    <p>{{ user.name }}</p>
    <p>{{ user.phone }}</p>
    <p>{{ user.website }}</p>
    <p>{{ user.company.name }}</p>
  </div>
</template>

<script>
export default {
  name: 'UserId',
  async asyncData({ route, $axios }) {
    const user = await $axios.$get(`/users/${route.params.id}`)
    return { user }
  },
}
</script>
