<template>
  <list></list>
</template>

<script>
import List from './components/List'

export default {
  name: 'app',
  components: {
    List
  }
}
</script>

<style lang="scss">
  *,
  *::after,
  *::before {
    margin: 0;
    padding: 0;

    box-sizing: inherit;
  }

  html {
    font-size: 62.5%;
  }

  body {
    box-sizing: border-box;

    font-family: 'Open Sans', sans-serif;
  }

  .pac-container {
    width: 100% !important;
    top: 65px !important;
    left: 0 !important;
  }

  .pac-item {
    padding: 15px 7px;

    span {
      font-size: 15px;
    }

    .pac-icon {
      display: none;
    }

    .pac-item-query {
      display: block;
      font-size: 18px

      span {
        font-size: 18px;
      }
    }
  }
</style>
