<template>
  <section class="theOnBoardingReferralSharingEmail">
    <p>You can also send <strong>one free month</strong> via email, separate emails with semicolon « ; »</p>
    <textarea v-model="referralEmails" placeholder="amelie.dupont@gmail.com ; jeanmichel@gmail.com" />
    <div class="theOnBoardingReferralSharingEmail__actions">
      <button class="button button--primary button--hasIcon" :disabled="numberOfReferralEmails === 0">
        <img :src="SendIcon" alt="Send icon" />
        Send {{ numberOfReferralEmails }} email{{ numberOfReferralEmails > 1 ? 's' : '' }}
      </button>
      <button class="button button--secondary" @click="finishReferral">
        Done
      </button>
    </div>
  </section>
</template>

<script>
import SendIcon from '../../../static/icons/send-icon.svg'

export default {
  data: () => {
    return {
      referralEmails: null,
      SendIcon
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
.theOnBoardingReferralSharingEmail {
  margin-top: 24px;

  p {
    margin-bottom: 16px;
  }

  textarea {
    margin-bottom: 16px;
    min-height: 128px;
  }

  &__actions {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
  }
}
</style>
