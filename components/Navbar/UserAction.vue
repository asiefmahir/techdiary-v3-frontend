<template>
  <div v-click-away="closeDropdown">
    <div v-if="$auth.loggedIn">
      <div
        class="relative flex items-center"
        @click="dropDownOpen = !dropDownOpen"
      >
        <!-- When user have profile pic -->
        <div
          v-if="$auth.user.profilePhoto"
          class="w-8 h-8 mr-2 overflow-hidden rounded-full cursor-pointer"
        >
          <img
            v-if="$auth.user.profilePhoto"
            :src="$auth.user.profilePhoto"
            :alt="$auth.user.name"
          />
        </div>

        <!-- When user don't have profile pic -->
        <svg v-else
             class='w-10 h-10 mr-2 overflow-hidden text-gray-500 rounded-full cursor-pointer dark:text-gray-300'
             xmlns='http://www.w3.org/2000/svg'
             viewBox='0 0 20 20'
             fill='currentColor'
        >
          <path
            fill-rule='evenodd'
            d='M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-6-3a2 2 0 11-4 0 2 2 0 014 0zm-2 4a5 5 0 00-4.546 2.916A5.986 5.986 0 0010 16a5.986 5.986 0 004.546-2.084A5 5 0 0010 11z'
            clip-rule='evenodd'
          />
        </svg>

        <p class="text-lg cursor-pointer md:mr-2 dark:text-gray-300">
          {{ $auth.user.name }}
        </p>

        <svg
          style="transition: transform 200ms"
          class="cursor-pointer dark:text-gray-300"
          :class="[dropDownOpen && 'svgRotation']"
          width="16"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M19 9l-7 7-7-7"
          />
        </svg>
      </div>
      <!--======================================
        User action dropdown
    ==========================================-->
      <transition name="fade">
        <div v-if="dropDownOpen" class="user-action-dropdown">
          <nuxt-link
            :to="{
              name: 'username',
              params: { username: $auth.user.username },
            }"
            class="user-action-dropdown__item"
          >
            <svg
              class="fill-current user-action-dropdown__icon"
              viewBox="0 0 24 24"
              stroke-linecap="round"
              stroke-linejoin="round"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
              <circle cx="12" cy="7" r="4"></circle>
            </svg>

            <p class="user-action-dropdown__label">আমার প্রোফাইল</p>
          </nuxt-link>

          <nuxt-link
            :to="{ name: 'dashboard' }"
            class="user-action-dropdown__item"
          >
            <svg
              class="user-action-dropdown__icon"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"
              />
            </svg>
            <p class="user-action-dropdown__label">ড্যাসবোর্ড</p>
          </nuxt-link>

          <nuxt-link
            :to="{ name: 'dashboard-bookmarks' }"
            class="user-action-dropdown__item"
          >
            <svg
              class="user-action-dropdown__icon"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 5a2 2 0 012-2h10a2 2 0 012 2v16l-7-3.5L5 21V5z"
              />
            </svg>

            <p class="user-action-dropdown__label">বুকমার্ক সমূহ</p>
          </nuxt-link>

          <nuxt-link
            :to="{ name: 'dashboard-diaries-new' }"
            class="user-action-dropdown__item"
          >
            <svg
              class="user-action-dropdown__icon"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M12 6v6m0 0v6m0-6h6m-6 0H6"
              />
            </svg>

            <p class="user-action-dropdown__label">নতুন ডায়েরি</p>
          </nuxt-link>

          <nuxt-link
            :to="{ name: 'dashboard-settings' }"
            class="user-action-dropdown__item"
          >
            <svg
              class="user-action-dropdown__icon"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M11.49 3.17c-.38-1.56-2.6-1.56-2.98 0a1.532 1.532 0 01-2.286.948c-1.372-.836-2.942.734-2.106 2.106.54.886.061 2.042-.947 2.287-1.561.379-1.561 2.6 0 2.978a1.532 1.532 0 01.947 2.287c-.836 1.372.734 2.942 2.106 2.106a1.532 1.532 0 012.287.947c.379 1.561 2.6 1.561 2.978 0a1.533 1.533 0 012.287-.947c1.372.836 2.942-.734 2.106-2.106a1.533 1.533 0 01.947-2.287c1.561-.379 1.561-2.6 0-2.978a1.532 1.532 0 01-.947-2.287c.836-1.372-.734-2.942-2.106-2.106a1.532 1.532 0 01-2.287-.947zM10 13a3 3 0 100-6 3 3 0 000 6z"
                clip-rule="evenodd"
              />
            </svg>

            <p class="user-action-dropdown__label">সেটিং</p>
          </nuxt-link>
          <button class="flex items-center" @click="logout">
            <svg
              class="user-action-dropdown__icon"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M3 3a1 1 0 00-1 1v12a1 1 0 102 0V4a1 1 0 00-1-1zm10.293 9.293a1 1 0 001.414 1.414l3-3a1 1 0 000-1.414l-3-3a1 1 0 10-1.414 1.414L14.586 9H7a1 1 0 100 2h7.586l-1.293 1.293z"
                clip-rule="evenodd"
              />
            </svg>

            <p class="user-action-dropdown__label">লগ আউট</p>
          </button>
        </div>
      </transition>
    </div>
    <div v-else class="flex items-center space-x-1">
      <svg
        class="w-8 text-gray-600 dark:text-gray-300"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          fill-rule="evenodd"
          d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-6-3a2 2 0 11-4 0 2 2 0 014 0zm-2 4a5 5 0 00-4.546 2.916A5.986 5.986 0 0010 16a5.986 5.986 0 004.546-2.084A5 5 0 0010 11z"
          clip-rule="evenodd"
        />
      </svg>
      <p class="text-lg text-gray-900 dark:text-gray-300">আগন্তুক</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'user-action',
  data: () => ({
    dropDownOpen: false,
  }),
  methods: {
    logout() {
      this.$auth.logout()
    },
    closeDropdown() {
      this.dropDownOpen = false
    },
  },
}
</script>

<style lang='scss'>
.user-action-dropdown {
  @apply absolute right-0 w-48 p-4 mt-1 bg-white rounded-bl rounded-br shadow-lg dark:bg-gray-700 top-full;
  &__item {
    @apply flex items-center mb-2 transition duration-150;
  }

  &__icon {
    @apply mr-2 text-gray-700 dark:text-gray-300 w-5;
  }

  &__label {
    @apply text-gray-800 dark:text-gray-300;
  }
}

.svgRotation {
  transform: rotateX(180deg);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 300ms;
}

.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
