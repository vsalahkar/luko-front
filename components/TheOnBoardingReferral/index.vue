<template>
  <article class="theOnBoardingReferral">
    <header class="theOnBoardingReferral__header">
      <h1>
        {{ user.firstName }}
        <base-user-profile-picture
          class="theOnBoardingReferral__profilePicture"
          :user-first-name="user.profilePicture"
        />
      </h1>
      <p>
        Don’t forget that for each new subscriber you refer, both you and them get <strong>one free month</strong> of
        coverage! 💙
      </p>
    </header>
    <the-on-boarding-referral-sharing-social :referral-code="user.referralCode" />
    <the-on-boarding-referral-sharing-email />
  </article>
</template>

<script>
import BaseUserProfilePicture from '../utils/BaseUserProfilePicture'
import ProfilePicture from '../../static/images/emma-photo.png'

import TheOnBoardingReferralSharingSocial from './TheOnBoardingReferralSharingSocial'
import TheOnBoardingReferralSharingEmail from './TheOnBoardingReferralSharingEmail'

export default {
  components: {
    BaseUserProfilePicture,
    TheOnBoardingReferralSharingSocial,
    TheOnBoardingReferralSharingEmail
  },
  props: {
    user: {
      default: () => {},
      type: Object
    }
  },
  data: () => {
    return {
      ProfilePicture
    }
  }
}
</script>

<style lang="scss">
.theOnBoardingReferral {
  margin: auto;
  width: 100%;
  max-width: 728px;

  &__header {
    h1 {
      position: relative;
      margin-bottom: 6px;
      font-weight: 900;
      font-size: 16px;
    }
  }

  &__profilePicture {
    position: absolute;
    top: 0;
    left: calc(-48px - 16px);
  }
}
</style>
