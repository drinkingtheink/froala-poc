<template>
  <section>
    <h3>Edit Your Header</h3>

    <section class="section-toolbar">
      <label for="heightVal">Height:</label>
      <input id="heightVal" type="number" v-model="heightVal" /><span>px</span>
    </section>

    <section class="header-output-wrapper">
      <header 
        ref="headerOutput" 
        v-bind:style="outputStyles" 
        class="header-output"
      >
        <img class="header-logo" alt="Your logo" src="../assets/okta-logo.png">
        <!--<froala :tag="img" v-model="imgModel"></froala>-->
      </header>
    </section>

    <section class="markup-output">
      <pre><code>{{headerMarkup}}</code></pre>
    </section>
  </section>
</template>

<script>

export default {
  name: 'EditHeader',
  data () {
    return {
      heightVal: 50,
      backgroundColor: '#333',
      imgSrc: '/assets/okta-logo.png',
      publicPath: process.env.BASE_URL,
      headerMarkup: null
    }
  },
  computed: {
    outputStyles() {
      let styleBlock = {
        height: `${this.heightVal}px`,
        backgroundColor: this.backgroundColor
      }
      return styleBlock;
    },
    logoSrc() {
      return `${this.publicPath}okta-logo.png`
    },
    logoModel() {
      let newModel = {
        src: `${this.publicPath}okta-logo.png`
      }

      return newModel;
    },
  },
  methods: {
    setHeaderMarkup() {
      this.headerMarkup = this.$refs.headerOutput.outerHTML;
    }
  },
  watch: {
    heightVal: function () {
      this.setHeaderMarkup();
    },
  },
  mounted() {
    this.setHeaderMarkup();
  }
};

</script>

<style lang="scss" scoped>
.section-toolbar {
  padding: 1rem;
}

.header-output-wrapper {
  background-color: #eaeaea;
  padding-bottom: 1rem;
}

.header-output {
  box-shadow: 1px 5px 10px 1px rgba(0,0,0,0.37);
  display: flex;
  align-items: center;
  padding: 0 1rem;

  .header-logo {
    height: 4em;
  }

  pre code {
    background-color: #eee;
    border: 1px solid #999;
    display: block;
    padding: 20px;
  }
}
</style>