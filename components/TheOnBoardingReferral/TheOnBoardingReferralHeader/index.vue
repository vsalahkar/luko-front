<template>
  <header class="theOnBoardingReferralHeader">
    <h1>
      {{ userFirstName }}
      <base-user-profile-picture
        class="theOnBoardingReferralHeader__profilePicture"
        :user-first-name="userProfilePictureName"
      />
    </h1>
    <p>
      Don’t forget that for each new subscriber you refer, both you and them get <strong>one free month</strong> of
      coverage! 💙
    </p>
  </header>
</template>

<script>
import BaseUserProfilePicture from '../../utils/BaseUserProfilePicture'
export default {
  components: {
    BaseUserProfilePicture
  },
  props: {
    userFirstName: {
      type: String,
      default: ''
    },
    userProfilePictureName: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss">
.theOnBoardingReferralHeader {
  h1 {
    position: relative;
    margin-bottom: 6px;
    font-weight: 900;
    font-size: 16px;
  }

  &__profilePicture {
    position: absolute;
    top: 0;
    left: calc(-48px - 16px);
  }
}
</style>
