<script>
// Appel du composant AppHome
import AppHome from './components/AppHome.vue'

export default {
  components: {
    AppHome
  }
}
</script>

<template>
  <div>
    <AppHome />
    <router-view></router-view>
  </div>
</template>
