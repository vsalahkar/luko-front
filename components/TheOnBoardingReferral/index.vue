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
    <the-on-boarding-referral-social-sharing :referral-code="user.referralCode" />
    <section class="theOnBoardingReferral__sharingEmail ">
      <p>You can also send <strong>one free month</strong> via email, separate emails with semicolon « ; »</p>
      <textarea v-model="referralEmails" placeholder="amelie.dupont@gmail.com ; jeanmichel@gmail.com" />
    </section>
    <footer class="theOnBoardingReferral__actions">
      <button class="button button--primary button--hasIcon" :disabled="numberOfReferralEmails === 0">
        <img :src="SendIcon" alt="" />
        Send {{ numberOfReferralEmails }} email{{ numberOfReferralEmails > 1 ? 's' : '' }}
      </button>
      <button class="button button--secondary" @click="finishReferral">
        Done
      </button>
    </footer>
  </article>
</template>

<script>
import BaseUserProfilePicture from '../utils/BaseUserProfilePicture'

import SendIcon from '../../static/icons/send-icon.svg'
import ProfilePicture from '../../static/images/emma-photo.png'

import TheOnBoardingReferralSocialSharing from './TheOnBoardingReferralSocialSharing'

export default {
  components: {
    BaseUserProfilePicture,
    TheOnBoardingReferralSocialSharing
  },
  props: {
    user: {
      default: () => {},
      type: Object
    }
  },
  data: () => {
    return {
      referralEmails: null,
      SendIcon,
      ProfilePicture
    }
  },
  computed: {
    emailsArray() {
      if (!this.referralEmails) {
        return []
      }

      const emailRegexp = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/

      return this.referralEmails
        .split(';')
        .map((email) => email.trim())
        .filter((email) => emailRegexp.test(email))
    },
    numberOfReferralEmails() {
      return this.emailsArray.length
    }
  },
  methods: {
    finishReferral() {
      console.info('Done')
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

  &__sharingEmail {
    margin-top: 24px;

    p {
      margin-bottom: 16px;
    }
  }

  &__sharingEmail {
    textarea {
      margin-bottom: 16px;
      min-height: 128px;
    }
  }

  &__actions {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
  }
}
</style>
