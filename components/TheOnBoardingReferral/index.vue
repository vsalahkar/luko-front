<template>
  <article class="theOnBoardingReferral">
    <header class="theOnBoardingReferral__header">
      <h1>
        Emma
        <img :src="ProfilePicture" alt="" />
      </h1>
      <p>
        Don’t forget that for each new subscriber you refer, both you and them
        get <strong>one free month</strong> of coverage! 💙
      </p>
    </header>
    <section class="theOnBoardingReferral__sharingSocial">
      <p>Share your <strong>one free month</strong> referral code</p>
      <div class="theOnBoardingReferral__shareActions">
        <div class="theOnBoardingReferral__referralCode">
          <span>SHARETHELOVE+5WMXM</span>
          <button class="button button--primary button--hasIcon">
            <img :src="CopyIcon" alt="copy paste icon" />
            Copy code
          </button>
        </div>
        <button class="button button--primary button--hasIcon">
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
      <p>
        You can also send <strong>one free month</strong> via email, separate
        emails with semicolon «;»
      </p>
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
import TwitterIcon from '../../static/icons/twitter-icon.svg'
import FacebookIcon from '../../static/icons/facebook-icon.png'
import SendIcon from '../../static/icons/send-icon.svg'
import CopyIcon from '../../static/icons/copy-icon.svg'
import ProfilePicture from '../../static/images/emma-photo.png'

export default {
  data: () => {
    return {
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

    img {
      position: absolute;
      top: 0;
      left: calc(-48px - 16px);
      width: 48px;
      height: 48px;
      border-radius: 100%;
    }
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
      border-top-left-radius: 0;
      border-bottom-left-radius: 0;
      cursor: copy;
    }
  }

  &__sharingEmail {
    textarea {
      margin-bottom: 16px;
      border: 1px solid $base-color-light-1;
      border-radius: 4px;
      padding: 12px 24px;
      width: 100%;
      max-width: 100%;
      min-width: 100%;
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
