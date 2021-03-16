<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" />
    </transition>
    <Todos @badValue="triggerToast" />
    <transition name="fada">
      <div v-if="showP">hola putos</div>
    </transition>
    <button @click="showP = !showP">toggle</button>
  </div>
</template>

<script>
import { ref } from "vue";
import Toast from "../components/Toast";
import Todos from "../components/Todos";

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false);
    const showP = ref(false);
    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => (showToast.value = false), 3000);
    };

    return { showToast, triggerToast, showP };
  },
};
</script>

<style>
.fada-enter-from {
  opacity: 0;
}
/* .fada-enter-to{opacity: 1;} */
.fada-enter-active {
  transition: all 1s ease;
}
.fada-leave-from {
  opacity: 1;
}
.fada-leave-to {
  opacity: 0;
}
.fada-leave-active {
  transition: all 1s ease;
}
/* toast */
/* .toast-enter-from {
  opacity: 0;
  transform: translateY(-60px);
}
.toast-enter-to {
  opacity: 1;
  transform: translateY(0);
} */
.toast-enter-active {
  /* transition: all .3s ease; */
  animation: wobble .5s ease;
}

.toast-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.toast-leave-to {
  opacity: 0;
  transform: translateY(-60px);
}
.toast-leave-active {
  transition: all .3s ease;
}
@keyframes wobble {
  0%{transform: translateY(-60px); opacity: 0;}
  50%{transform: translateY(0px); opacity: 1;}
  60%{transform: translateX(8px);}
  70%{transform: translateX(-8px);}
  80%{transform: translateX(4px);}
  90%{transform: translateX(-4px);}
  100%{transform: translateX(0px);}
}
</style>