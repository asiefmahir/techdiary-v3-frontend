<template>
  <div class="mb-10 bg-white rounded-md dark:bg-gray-900">
    <div class="flex items-center space-x-2">
      <img
        :src="$auth.user.profilePhoto"
        :alt="$auth.user.username"
        class="w-8 rounded-full"
        v-if="$auth.loggedIn"
      />

      <svg
        v-if="!$auth.loggedIn"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
        fill="currentColor"
        class="w-8 text-gray-600 dark:text-gray-300"
        data-v-2012b195=""
      >
        <path
          fill-rule="evenodd"
          d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-6-3a2 2 0 11-4 0 2 2 0 014 0zm-2 4a5 5 0 00-4.546 2.916A5.986 5.986 0 0010 16a5.986 5.986 0 004.546-2.084A5 5 0 0010 11z"
          clip-rule="evenodd"
          data-v-2012b195=""
        ></path>
      </svg>

      <span class="text-base dark:text-gray-300" v-if="$auth.loggedIn">{{
        $auth.user.name
      }}</span>

      <span class="text-base dark:text-gray-300" v-if="!$auth.loggedIn">
        আগন্তুক
      </span>
    </div>

    <div
      class="flex p-5 mt-3 text-lg transition-all duration-150 bg-gray-100 border border-gray-200 rounded-lg cursor-pointer dark:border-gray-500 dark:bg-gray-600 hover:bg-white"
      @click="go"
    >
      <svg
        class="w-6 h-6 mr-4 text-gray-700 opacity-75 fill-current dark:text-gray-300"
        viewBox="0 0 512 512"
      >
        <path
          d="M384 250v12c0 6.6-5.4 12-12 12h-98v98c0 6.6-5.4 12-12 12h-12c-6.6 0-12-5.4-12-12v-98h-98c-6.6 0-12-5.4-12-12v-12c0-6.6 5.4-12 12-12h98v-98c0-6.6 5.4-12 12-12h12c6.6 0 12 5.4 12 12v98h98c6.6 0 12 5.4 12 12zm120 6c0 137-111 248-248 248S8 393 8 256 119 8 256 8s248 111 248 248zm-32 0c0-119.9-97.3-216-216-216-119.9 0-216 97.3-216 216 0 119.9 97.3 216 216 216 119.9 0 216-97.3 216-216z"
        ></path>
      </svg>
      <p class="text-gray-700 dark:text-gray-300">নতুন ডায়েরি লিখুন 😍</p>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    go() {
      if (this.$auth.loggedIn) {
        this.$router.push({ name: 'dashboard-diaries-new' })
      } else {
        this.$store.commit(
          'alert/ERROR_ALERT',
          '<b>নতুন ডায়েরি লিখতে আপনাকে অবশ্যই আগে লগইন করতে হবে।</b>'
        )
      }
    },
  },
}
</script>
