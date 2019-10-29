<template>
  <main>
    <the-header />
    <section class="container">
      <the-on-boarding-referral :user="User" />
    </section>
  </main>
</template>

<script>
import TheHeader from '../components/TheHeader'
import TheOnBoardingReferral from '../components/TheOnBoardingReferral'

import User from '../api/user'

export default {
  components: {
    TheHeader,
    TheOnBoardingReferral
  },
  data: () => {
    return {
      User
    }
  }
}
</script>

<style lang="scss"></style>
