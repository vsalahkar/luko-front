<template>
  <div class="baseProfilePicture">
    <img :src="userProfilePictureUrl" :alt="`${userFirstName} logo`" />
  </div>
</template>

<script>
export default {
  props: {
    userFirstName: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      userProfilePictureUrl: this.loadUserProfilePicture(this.userFirstName)
    }
  },
  methods: {
    loadUserProfilePicture(firstName) {
      return require(`~/static/images/${firstName}-photo.png`)
    }
  }
}
</script>

<style lang="scss">
.baseProfilePicture {
  overflow: hidden;
  border-radius: 100%;
  width: 48px;
  height: 48px;

  img {
    width: 100%;
    height: 100%;
  }
}
</style>
