<template lang="pug">
  div.main-wrape
      div.container 
        div.row 
          div.content
            logo
            h3.title NUXT-ACTION-GITHUB-PAGES
      
</template>
<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  }
}
</script>

<style scope lang="scss">
.content {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 6rem;
}
h3 {
  margin-top: 2rem;
}
</style>
