<template>
  <article class="theOnBoardingReferral">
    <the-on-boarding-referral-header
      :user-first-name="user.firstName"
      :user-profile-picture-name="user.profilePicture"
    />
    <the-on-boarding-referral-sharing-social :referral-code="user.referralCode" />
    <the-on-boarding-referral-sharing-email />
  </article>
</template>

<script>
import TheOnBoardingReferralHeader from './TheOnBoardingReferralHeader'
import TheOnBoardingReferralSharingSocial from './TheOnBoardingReferralSharingSocial'
import TheOnBoardingReferralSharingEmail from './TheOnBoardingReferralSharingEmail'

export default {
  components: {
    TheOnBoardingReferralHeader,
    TheOnBoardingReferralSharingSocial,
    TheOnBoardingReferralSharingEmail
  },
  props: {
    user: {
      default: () => {},
      type: Object
    }
  }
}
</script>

<style lang="scss">
.theOnBoardingReferral {
  margin: auto;
  padding-top: 48px;
  width: 100%;
  max-width: 728px;
}
</style>
