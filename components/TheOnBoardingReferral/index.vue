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
    <section class="theOnBoardingReferral__sharingSocial">
      <p>Share your <strong>one free month</strong> referral code</p>
      <div class="theOnBoardingReferral__shareActions">
        <div class="theOnBoardingReferral__referralCode">
          <span>{{ user.referralCode }}</span>
          <button class="button button--primary button--hasIcon" @click="copyToClipboard(user.referralCode)">
            <img :src="CopyIcon" alt="copy paste icon" />
            Copy code
            <transition name="fade-bottom">
              <base-toast
                v-if="isCopiedToClipboard"
                class="referralCode__confirmationToast"
                description="📋 Referral code copied!"
              />
            </transition>
          </button>
        </div>
        <button class="button button--primary button--hasIcon" @click="shareWithTwitter">
          <img :src="TwitterIcon" alt="copy paste icon" />
          Tweet
        </button>
        <button class="button button--primary button--hasIcon">
          <img :src="FacebookIcon" alt="copy paste icon" />
          Share
        </button>
      </div>
    </section>
    <section class="theOnBoardingReferral__sharingEmail ">
      <p>You can also send <strong>one free month</strong> via email, separate emails with semicolon «;»</p>
      <textarea placeholder="amelie.dupont@gmail.com ; jeanmichel@gmail.com" />
    </section>
    <footer class="theOnBoardingReferral__actions">
      <button class="button button--primary button--hasIcon" disabled>
        <img :src="SendIcon" alt="" />
        Send 0 email
      </button>
      <button class="button button--secondary" @click="finishReferral">
        Done
      </button>
    </footer>
  </article>
</template>

<script>
import BaseUserProfilePicture from '../utils/BaseUserProfilePicture'

import TwitterIcon from '../../static/icons/twitter-icon.svg'
import FacebookIcon from '../../static/icons/facebook-icon.png'
import SendIcon from '../../static/icons/send-icon.svg'
import CopyIcon from '../../static/icons/copy-icon.svg'
import ProfilePicture from '../../static/images/emma-photo.png'
import BaseToast from '../utils/BaseToast'

export default {
  components: {
    BaseToast,
    BaseUserProfilePicture
  },
  props: {
    user: {
      default: () => {},
      type: Object
    }
  },
  data: () => {
    return {
      isCopiedToClipboard: false,
      TwitterIcon,
      FacebookIcon,
      SendIcon,
      CopyIcon,
      ProfilePicture
    }
  },
  methods: {
    finishReferral() {
      console.info('Done')
    },
    async copyToClipboard(stringToCopy) {
      try {
        await navigator.clipboard.writeText(stringToCopy)
        this.toggleCopyToClipboardToast()
      } catch (err) {
        console.error('Failed to copy: ', err)
      }
    },
    toggleCopyToClipboardToast() {
      if (this.isCopiedToClipboard) {
        return
      }

      this.isCopiedToClipboard = true

      setTimeout(() => {
        this.isCopiedToClipboard = false
      }, 2000)
    },
    shareWithTwitter() {
      const initialWindowWith = window.outerWidth
      const targetWindowWidth = 550
      const targetWindowXPosition = initialWindowWith / 2 - targetWindowWidth / 2

      const targetWindowHeight = 550
      const targetWindowPositionFromTop = 100

      const strWindowFeatures = `
      width= ${targetWindowWidth},
      height= ${targetWindowHeight},
      left=${targetWindowXPosition},
      top=${targetWindowPositionFromTop}
      `
      window.open(this.tweetUrlWithContent, 'New tweet', strWindowFeatures)
    }
  },
  computed: {
    tweetUrlWithContent() {
      const tweetText =
        "Je vous partage mon code promo qui permet de bénéficier d'un mois gratuit chez la néo-assurance Luko :"
      return `https://twitter.com/intent/tweet?text=${tweetText} ${this.user.referralCode}`
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

  &__sharingSocial,
  &__sharingEmail {
    margin-top: 24px;

    p {
      margin-bottom: 16px;
    }
  }

  &__shareActions {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;

    & > button {
      margin-left: 8px;
    }
  }

  &__referralCode {
    flex: 1;
    display: flex;
    align-items: stretch;

    span {
      border-top-left-radius: 4px;
      border-bottom-left-radius: 4px;
      padding: 12px 24px;
      background-color: $secondary-color;
      display: flex;
      align-items: center;
      flex: 1;
      color: $primary-color;
    }

    button {
      position: relative;
      border-top-left-radius: 0;
      border-bottom-left-radius: 0;
      cursor: copy;
    }
  }

  .referralCode {
    &__confirmationToast {
      left: 50%;
      transform: translate(-50%, 0);
      bottom: 100%;
      margin-bottom: 4px;
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
