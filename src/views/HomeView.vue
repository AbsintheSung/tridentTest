<script setup>
import { ref, computed, onMounted } from 'vue'
import LoGo from '@/components/LoGo.vue'
import NavBar from '@/components/NavBar.vue'
import { characteristic as charData } from '@/content/characteristicText'
const isOpen = ref(false)
const isLoading = ref(true)
const bgImgRef = ref(null)
const toggleMenu = () => {
  isOpen.value = !isOpen.value
}
const getCharData = computed(() => {
  return charData.map((item) => ({
    title: item.title.split(''),
    content: item.content,
  }))
})

const imgLoadingFinish = (url) => {
  const img = new Image()
  img.src = url
  img.onload = () => {
    isLoading.value = false
    bgImgRef.value.style.backgroundImage = `url(${url})`
  }
}

onMounted(() => {
  const imageUrl =
    'https://s3-alpha-sig.figma.com/img/0411/a36a/2789ca730221661c9008e0bf404c1cdc?Expires=1742774400&Key-Pair-Id=APKAQ4GOSFWCW27IBOMQ&Signature=a31lbs6VVz5bxHCa9XvR-BcBnYDGXhHIDp17zYJ05UpQKeCA2SS3WNBK3ZarsofoKzp2ZolFKVhCPYJ9BGLpQNtUByTgTc9PSoZT7-ydRm3kOzpv0y0h5FJg2X~i2jMb2Sb1caWQ2tWpC-ZZ2dTCOhYHRf4j49~Sxe-2Iw5k3ZgXV9f-I4WJPtDVFpyV6GmMDI~JSk47hmxheTNG26-ai396851vBcTl4o4D~RvraeNVFFUcLa-1FwDdDZ-MQGcPXj5rE4PG4nYDfGE5s9H9pICYQUkOwiZ2dyx~HOza98hjdMHeolrcyLrDCDIaRgVbPkN1clgmONBfFbZR~OzDgA__'
  imgLoadingFinish(imageUrl)
})
</script>

<template>
  <div class="flex flex-col h-full">
    <header>
      <NavBar :isOpen="isOpen" :toggleMenu="toggleMenu">
        <template #logo>
          <h1 class="shadow-sm rounded-full bg-white text-black">
            <LoGo />
          </h1>
        </template>
      </NavBar>
    </header>
    <main class="flex-1">
      <div class="container flex">
        <aside class="relative hidden md:block md:w-1/4 p-10 lg:p-16">
          <h1
            class="absolute -right-0 translate-x-1/2 scale-[1.5] shadow-md rounded-full bg-white text-black"
          >
            <LoGo />
          </h1>
          <h3 class="pb-16 font-bold text-3xl text-center">白頭翁不吃小米</h3>
          <ul class="text-lg space-y-5">
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
        </aside>
        <section class="w-fill md:w-3/4 flex flex-col">
          <div
            ref="bgImgRef"
            :class="{ skeleton: isLoading }"
            class="main-bg flex-col space-y-1 pt-24 ps-15 pe-6 pb-9 sm:pt-80 lg:pt-125 lg:px-10 text-white"
          >
            <h2 class="mt-auto text-end font-bold text-5xl">白頭翁 (Chinese bulbul)</h2>
            <p class="text-end text-lg">
              又名白頭鵯。以果實、昆蟲為主食，無法消化小米、穀類。平均壽命約 8~10 年。
            </p>
          </div>
          <div class="bg-[#DCCCBC] mt-auto py-12 px-9 lg:py-14 lg:px-12">
            <ul class="flex flex-col gap-y-12 md:gap-x-8 lg:flex-row lg:gap-x-18">
              <li class="flex gap-x-9" v-for="charItem in getCharData" :key="charItem.title">
                <h4 class="text-4xl font-bold">
                  <template v-for="(titleItem, index) in charItem.title" :key="titleItem + index">
                    <span :class="{ circles: index === charItem.title.length - 1 }">
                      {{ titleItem }}
                    </span>
                  </template>
                </h4>
                <p>{{ charItem.content }}</p>
              </li>
            </ul>
          </div>
        </section>
      </div>
    </main>
    <footer></footer>
  </div>
</template>

<style scoped>
.skeleton {
  background-color: #e2e2e2;
  background-size: 100%;
}

.main-bg {
  background-position: 60% 60%;
  background-repeat: no-repeat;
  background-size: 200%;
}
.circles {
  position: relative;
  z-index: 1;
}
.circles:after {
  position: absolute;
  z-index: -1;
  content: '';
  width: 25px;
  height: 25px;
  border-radius: 50%;
  border: 8px solid #aa6666;
  background-color: transparent;
  bottom: 0;
  transform: translateX(-10px);
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
