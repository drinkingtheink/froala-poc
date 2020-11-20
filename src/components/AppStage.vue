<template>
  <div>
    <section id="compose">
      <h2>Edit Your Content</h2>
      <EditHeader 
        :colorOptions="colorOptions"
        v-on:headerMarkupChanged="updateHeaderMarkup"
      />
      <EditBody />
    </section>

    <section id="display">
      <MarkupDisplay :headerMarkup="headerMarkup" />
    </section>
  </div>
</template>

<script>
import EditHeader from './EditHeader.vue'
import EditBody from './EditBody.vue'
import MarkupDisplay from './MarkupDisplay.vue'
import colors from '../fixtures/colors';

export default {
  name: 'AppStage',
  data() {
    return {
      colorOptions: colors,
      headerMarkup: null
    }
  },
  components: {
    EditHeader,
    EditBody,
    MarkupDisplay
  },
  methods: {
    updateHeaderMarkup(markup) {
      this.headerMarkup = markup;
    }
  }
};
</script>

<style lang="scss" scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
