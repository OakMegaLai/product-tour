<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import { onMounted, ref } from 'vue'

const imageUrl = ref('')

onMounted(() => {
  setMeta()
  fakeToFetchSomeData()
})

function setMeta() {
  document.title = 'Vue 3 Vite'
  const metaTags = [
    { name: 'description', content: '這是一個示範網站，提供豐富的資訊。' },
    { name: 'keywords', content: '示範, 網站, 資訊' },
    { name: 'author', content: '你的名字或公司名稱' },
    { property: 'og:title', content: '示範網站標題' },
    { property: 'og:description', content: '這是一個用於展示的示範網站。' },
    { property: 'og:image', content: 'https://example.com/image.jpg' },
    { property: 'og:url', content: 'https://example.com' }
  ]

  metaTags.forEach((tag) => {
    const metaElement = document.createElement('meta')
    Object.keys(tag).forEach((key) => {
      metaElement.setAttribute(key, tag[key])
    })
    document.head.appendChild(metaElement)
  })
}

function fakeToFetchSomeData() {
  setTimeout(() => {
    imageUrl.value =
      'https://e8a87cd35421b61893e89341d469998aed92254a.mdnplay.dev/en-US/docs/Web/SVG/Element/image/mdn_logo_only_color.png'
  }, 5000)
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
    <img v-if="imageUrl" alt="Vue logo" class="logo" :src="imageUrl" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!!!" />
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
