<template>
  <div class="contact">
    <h1>Contact</h1>
    <button @click="toggleShow">
      Show
    </button>
    <p v-text="showThis"></p>
    <div v-if="showThis">

    <transition-group appear tag="ul" name="stagger" >
      <li
        :style="{ '--i': index }"
        v-for="(icon, index) in icons"
        :key="icon.name"
      >
        <span class="material-icons">{{ icon.name }}</span>
        <div>{{ icon.text }}</div>
      </li>
    </transition-group>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const icons = ref([
      { name: "alternate_email", text: "by email" },
      { name: "local_phone", text: "by phone" },
      { name: "local_post_office", text: "by post" },
      { name: "local_fire_department", text: "by smoke signal" },
    ]);
    const showThis = ref(true)
    const toggleShow = () => {
      showThis.value = !showThis.value
    }
    
    return { icons, showThis, toggleShow };
  },
};
</script>

<style>
.contact ul {
  padding: 0;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  max-width: 400px;
  margin: 60px auto;
}
.contact li {
  list-style-type: none;
  background: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  line-height: 1.5em;
  /* transition: all.2s; */
}
.contact li:hover{
  transform: scale(1.02);
}
.stagger-enter-from,
.stagger-leave-to {
  opacity: 0;
  transform: translateX(20px);
}
.stagger-enter-to,
.stagger-leave-from {
  opacity: 1;
  transform: translateX(0);
}
.stagger-enter-active{
  transition: all 0.5s ease;
  transition-delay: calc(.2s * (var(--i)));
}
.stagger-leave-active{
  transition: all 0.3s ease;
  transition-delay: calc(2s * (var(--i)));
}
</style>