<script setup>
import { onMounted, computed } from "vue";
import { useUserStore } from "../../stores/user";
import Authbutton from "./Authbutton.vue";
import Logo from "./Logo.vue";
import NavigationLinks from "./NavigationLinks.vue";
import UserInfo from "./UserInfo.vue";

const userStore = useUserStore();
const getUser = computed(() => userStore.getUser);
const isLoggedIn = computed(() => userStore.isLoggedIn);
const user = computed(() => userStore.user);

onMounted(() => {
  userStore.fetchUser();
});
</script>

<template>
  <nav
    class="bg-white border-gray-200 px-2 sm:px-4 py-2.5 rounded dark:bg-gray-800"
  >
    <div
      class="container flex flex-wrap items-center justify-between mx-auto my-2"
    >
      <Logo />
      <UserInfo v-if="isLoggedIn" :user="user.data" />
      <Authbutton v-else />
      <NavigationLinks />
    </div>
  </nav>
</template>
