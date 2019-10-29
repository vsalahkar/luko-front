<template>
  <section class="container">
    <header class="theHeader">
      <div class="theHeader__heading">
        <img :src="lukoLogo" alt="" />
        <span>Protect your nest</span>
      </div>
      <div class="theHeader__actions">
        <a class="link link--primary" href="#">Logout</a>
        <span>John Doe</span>
      </div>
    </header>
  </section>
</template>

<script>
import lukoLogo from '../../static/logo/luko.svg'

export default {
  data: () => {
    return {
      lukoLogo
    }
  }
}
</script>

<style lang="scss">
.theHeader {
  padding: 28px 0;
  display: flex;
  align-items: center;
  justify-content: space-between;

  &__heading {
    display: flex;
    align-items: center;

    img {
      max-width: 53px;
    }

    span {
      margin-left: 16px;
      color: $base-color-dark-1;
    }
  }

  &__actions {
    span {
      margin-left: 24px;
      font-weight: 900;
      color: $primary-color;
    }
  }
}
</style>
