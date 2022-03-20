<template>
  <div class="flex flex-col items-center">
    <h1 class="p-4 bg-green-700 rounded-md">
      List of users ordered by their according message
    </h1>
    <!-- <pre>{{ messages }}</pre> -->
    <section>
      <div v-for="user in groupedMessages" :key="user.id" class="mt-4">
        <p>
          User: <b>{{ user.name }}</b>
        </p>

        <aside>
          Messages:
          <span v-if="!user.messages.length">No messages actually</span>
        </aside>
        <p v-for="message in user.messages" :key="message.id">
          <span class="italic">- {{ message.text }}</span>
        </p>
      </div>
    </section>
  </div>
</template>

<script>
// ES version of lodash, lighter overall
import { cloneDeep } from 'lodash-es'

export default {
  name: 'Index',
  data() {
    return {
      messages: [
        {
          id: 1,
          text: 'Hello world',
          userId: 1,
        },
        {
          id: 2,
          text: 'Nice cool message',
          userId: 1,
        },
        {
          id: 3,
          text: 'Still for the first user?',
          userId: 1,
        },
        {
          id: 4,
          text: 'Yep, apparently...',
          userId: 1,
        },
        {
          id: 5,
          text: "Eh, surprise, I'm a sneaky one...",
          userId: 3,
        },
        {
          id: 6,
          text: 'Oh, a second one.',
          userId: 2,
        },
        {
          id: 7,
          text: "You're damn right!!",
          userId: 2,
        },
      ],
      users: [
        {
          name: 'Patrick',
          id: 1,
          messages: [],
        },
        {
          name: 'Pablo',
          id: 2,
          messages: [],
        },
        {
          name: 'Unkown author',
          id: 5,
          messages: [],
        },
        {
          name: 'Escobar',
          id: 3,
          messages: [],
        },
      ],
    }
  },
  computed: {
    groupedMessages() {
      // we use that to avoid any kind of further mutation to the initial `users` array
      const clonedUsers = cloneDeep(this.users)
      // we do loop on each message and find a corresponding user for it
      this.messages.forEach((message) =>
        clonedUsers.forEach((user) => {
          if (user.id === message.userId) {
            user.messages.push(message)
          }
        })
      )
      return clonedUsers
    },
  },
}
</script>

<style>
* {
  @apply bg-gray-800 text-gray-100;
}
</style>
