<template>
  <section>
    <h2>Edit Your Content</h2>
    <EditHeader :colorOptions="colorOptions" />
  </section>
</template>

<script>
import EditHeader from './EditHeader.vue'
import colors from '../fixtures/colors';

export default {
  name: 'AppStage',
  data() {
    return {
      colorOptions: colors
    }
  },
  components: {
    EditHeader
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
