<template>
  <section>
    <h2>Edit Your Content</h2>
    <EditHeader />
  </section>
</template>

<script>
import EditHeader from './EditHeader.vue'

export default {
  name: 'AppStage',
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
