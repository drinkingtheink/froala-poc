<template>
  <section>
    <h3>Edit Your Header</h3>

    <section class="section-toolbar">
      <label for="heightVal">Height:</label>
      <input id="heightVal" type="number" v-model="heightVal" />
    </section>

    <header v-bind:style="outputStyles" id="header-output"></header>
  </section>
</template>

<script>

export default {
  name: 'EditHeader',
  data () {
    return {
      heightVal: 50,
      backgroundColor: 'red'
    }
  },
  computed: {
    outputStyles() {
      let styleBlock = {
        height: `${this.heightVal}px`,
        backgroundColor: this.backgroundColor
      }
      return styleBlock;
    }
  }
};

</script>