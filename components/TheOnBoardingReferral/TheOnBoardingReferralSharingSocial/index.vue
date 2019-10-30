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
          <span>Copy code</span>
          <transition name="fade-bottom">
            <base-toast
              v-click-outside.stop="closeCopyToClipboardToast"
              v-if="isCopiedToClipboard"
              class="referralCode__confirmationToast"
              description="📋 Referral code copied!"
            />
          </transition>
        </button>
      </div>
      <div class="theOnBoardingReferralSocialSharing__socialNetwork">
        <button class="button button--primary button--hasIcon" @click="shareWithTwitter">
          <img :src="TwitterIcon" alt="tweet icon" />
          <span>Tweet</span>
        </button>
        <button class="button button--primary button--hasIcon">
          <img :src="FacebookIcon" alt="facebook icon" />
          <span>Share</span>
        </button>
      </div>
    </div>
  </section>
</template>

<script>
import vClickOutside from 'v-click-outside'

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
  directives: {
    clickOutside: vClickOutside.directive
  },
  computed: {
    tweetUrlWithContent() {
      const twitterUrl = 'https://twitter.com/intent/tweet?text='
      const tweetText = `Je vous partage mon code promo qui permet de bénéficier d'un mois gratuit chez la néo-assurance Luko : ${this.referralCode}`

      return `${twitterUrl}${tweetText}`
    },
    windowFeatureParameters() {
      const initialWindowWidth = window.outerWidth
      const targetWindowWidth = 550
      const targetWindowXPosition = initialWindowWidth / 2 - targetWindowWidth / 2

      const targetWindowHeight = 550
      const targetWindowPositionFromTop = 100

      return `
      width= ${targetWindowWidth},
      height= ${targetWindowHeight},
      left=${targetWindowXPosition},
      top=${targetWindowPositionFromTop}
      `
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
      window.open(this.tweetUrlWithContent, 'New tweet', this.windowFeatureParameters)
    },
    closeCopyToClipboardToast() {
      if (!this.isCopiedToClipboard) {
        return
      }
      this.isCopiedToClipboard = false
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
    align-items: stretch;
    justify-content: space-between;
    flex-wrap: wrap;

    @media (max-width: 728px) {
      button {
        & > span {
          display: none;
        }

        & > img {
          margin: 0;
        }
      }
    }
  }

  &__referralCode {
    flex: 1;
    display: flex;
    align-items: stretch;

    & > span {
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

      &:hover {
        cursor: copy;
      }
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

  &__socialNetwork {
    display: flex;
    align-items: stretch;

    & > button {
      margin-left: 8px;
    }

    @media (max-width: 480px) {
      margin-top: 16px;
      width: 100%;

      button {
        margin: 0;
        flex: 1;

        &:first-of-type {
          margin-right: 8px;
        }

        & > span {
          display: inherit;
        }

        & > img {
          margin-right: 16px;
        }
      }
    }
  }
}
</style>
