<template>
  <section class="theOnBoardingReferralSocialSharing">
    <p class="theOnBoardingReferralSocialSharing__description">
      Share your <strong>one free month</strong> referral code
    </p>
    <div class="theOnBoardingReferralSocialSharing__actions">
      <div class="theOnBoardingReferralSocialSharing__referralCode">
        <span>{{ referralCode }}</span>
        <button class="button button--primary button--hasIcon" @click="copyToClipboard(referralCode)">
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
</template>

<script>
import BaseToast from '../../utils/BaseToast'

import TwitterIcon from '../../../static/icons/twitter-icon.svg'
import FacebookIcon from '../../../static/icons/facebook-icon.png'
import CopyIcon from '../../../static/icons/copy-icon.svg'

export default {
  components: {
    BaseToast
  },
  props: {
    referralCode: {
      type: String,
      default: ''
    }
  },
  data: () => {
    return {
      isCopiedToClipboard: false,
      TwitterIcon,
      FacebookIcon,
      CopyIcon
    }
  },
  computed: {
    tweetUrlWithContent() {
      const tweetText =
        "Je vous partage mon code promo qui permet de bénéficier d'un mois gratuit chez la néo-assurance Luko :"

      return `https://twitter.com/intent/tweet?text=${tweetText} ${this.referralCode}`
    }
  },
  methods: {
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
  }
}
</script>

<style lang="scss">
.theOnBoardingReferralSocialSharing {
  margin-top: 24px;

  &__description {
    margin-bottom: 16px;
  }

  &__actions {
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
      user-select: all;
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
}
</style>
