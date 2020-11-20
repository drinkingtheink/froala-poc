<template>
  <div id="composed-markup-display">
    <p v-if="showInfoMessage">-- We'll display your composed markup here -- </p>
    <div v-if="headerMarkup" v-html="headerMarkup" />
  </div>
</template>

<script>
export default {
  name: 'MarkupDisplay',
  props: ['headerMarkup'],
  computed: {
    showInfoMessage() {
      return !this.headerMarkup;
    }
  }
};
</script>

<style lang="scss" scoped>
  #composed-markup-display {
    min-height: 10rem;
    background-color: #eaeaea;
  }
</style>