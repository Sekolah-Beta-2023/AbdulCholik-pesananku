<template>
  <div>
    <NavbarHeader />
    <BottomNavbar />
    <Nuxt />
    <FooterAuthor />
  </div>
</template>

<script>
import NavbarHeader from '@/components/NavbarHeader.vue'
import FooterAuthor from '@/components/FooterAuthor.vue'
import BottomNavbar from '@/components/BottomNavbar.vue'

export default {
components: {
    NavbarHeader,
    FooterAuthor,
    BottomNavbar
}
}
</script>
