<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <router-link
      class="navbar-brand"
      :to="{ name: 'Home' }"
    >
      <!-- to="/" 페이지가 많아지면 유지보수가 힘들다. -->
      YS coder
    </router-link>
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <router-link
          class="nav-link"
          :to="{ name: 'Todos' }"
        >
          Todos
        </router-link>
      </li>
    </ul>
  </nav>
  <div class="container">
    <router-view />
  </div>
  <Transition name="slide">
    <Toast
      v-if="showToast"
      message="toastMessage"
      :type="toastAlertType"
    />
  </Transition>
</template>

<script>
import Toast from "@/components/Toast.vue";
import { useToast } from "@/composables/toast";

export default {
  components: { Toast },
  setup() {
    const { triggerToast, toastAlertType, toastMessage, showToast } =
      useToast();

    console.log(showToast.value);

    return {
      triggerToast,
      toastAlertType,
      toastMessage,
      showToast,
    };
  },
};
</script>

<style scoped>
.slide-enter-active,
.slide-leave-active {
  transition: all 0.5s ease;
}
.slide-enter-from,
.slide-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}
.slide-enter-to,
.slide-leave-from {
  opacity: 1;
  transform: translateY(0px);
}
</style>
