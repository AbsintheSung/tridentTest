<script setup>
defineProps({
  isOpen: {
    type: Boolean,
    default: false,
  },
  toggleMenu: {
    type: Function,
    default: () => {},
  },
})
</script>
<template>
  <nav class="container relative py-9 px-6 md:hidden">
    <div class="flex items-center">
      <button class="menu-bar" @click="toggleMenu">
        <div class="menu-bar-line" :class="{ 'menu-bar-line-open': isOpen }"></div>
      </button>
      <h2 class="absolute left-1/2 -translate-x-1/2 font-bold text-xl">白頭翁不吃小米</h2>
      <div class="ms-auto">
        <slot name="logo"></slot>
      </div>
    </div>
    <transition name="fade">
      <div
        v-show="isOpen"
        class="absolute top-full left-0 right-0 z-10 w-full bg-white shadow-lg md:hidden"
      >
        <ul class="text-lg space-y-5 pb-10">
          <li class="text-center">
            <RouterLink to="/" class="link">白頭翁的特性</RouterLink>
          </li>
          <li class="text-center">
            <RouterLink to="/story" class="link">白頭翁的故事</RouterLink>
          </li>
          <li class="text-center">
            <RouterLink to="/beautiful-photos" class="link">白頭翁的美照</RouterLink>
          </li>
          <li class="text-center">
            <RouterLink to="/crisis" class="link">白頭翁的危機</RouterLink>
          </li>
        </ul>
      </div>
    </transition>
  </nav>
</template>
<style scoped>
.menu-bar {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  width: 24px;
  height: 24px;
  transition: transform 0.3s ease-in-out;
}
.menu-bar-line {
  width: 50%;
  height: 4px;
  margin-right: auto;
  background-color: black;
  transition: background-color 0.3s ease-in-out;
}
.menu-bar-line:after {
  content: '';
  position: absolute;
  width: 100%;
  height: 4px;
  background-color: black;
  left: 0px;
  top: 20px;
  transition:
    transform 0.3s ease-in-out,
    top 0.3s ease-in-out;
}
.menu-bar-line:before {
  content: '';
  position: absolute;
  width: 100%;
  height: 4px;
  background-color: black;
  left: 0px;
  top: 0px;
  transition:
    transform 0.3s ease-in-out,
    top 0.3s ease-in-out;
}
/* 開啟時添加的 X 樣式 */
.menu-bar-line-open {
  background-color: transparent;
}

.menu-bar-line-open::before {
  top: 0;
  transform: rotate(45deg);
}

.menu-bar-line-open::after {
  top: 0;
  transform: rotate(-45deg);
}

.fade-enter-active,
.fade-leave-active {
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.router-link-exact-active {
  color: #aa6666;
  text-decoration: underline;
}
.link:hover {
  color: #aa6666;
  text-decoration: underline;
}
</style>
