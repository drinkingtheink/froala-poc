<template>
  <section>
    <h3>Edit Your Header</h3>

    <section class="section-toolbar">
      <div class="set-section set-height">
        <label for="heightVal">Height:</label>
        <input id="heightVal" type="number" v-model="heightVal" /><span>px</span>
      </div>

      <div class="set-section set-shadow">
        <button class="radio" v-on:click="toggleShadow">
          <span v-if="showShadow">Turn Off Shadow</span>
          <span v-else>Show Shadow</span>
        </button>
      </div>
    </section>

    <section class="header-output-wrapper">
      <header 
        ref="headerOutput" 
        v-bind:style="outputStyles" 
        class="header-output"
      >
        <img class="header-logo" alt="Your logo" src="../assets/okta-logo.png">
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
      heightFloor: 40,
      backgroundColor: '#333',
      imgSrc: '/assets/okta-logo.png',
      publicPath: process.env.BASE_URL,
      headerMarkup: null,
      showShadow: true
    }
  },
  computed: {
    outputStyles() {
      let styleBlock = {
        height: `${this.heightVal}px`,
        backgroundColor: this.backgroundColor,
        boxShadow: this.dropShadowStyles

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
    dropShadowStyles() {
      let shadowStyles = `1px 5px 10px 1px rgba(0,0,0,0.37)`
      return this.showShadow ? shadowStyles : 'none';
    }
  },
  methods: {
    setHeaderMarkup() {
      this.headerMarkup = this.$refs.headerOutput.outerHTML;
    },
    toggleShadow() {
      this.showShadow = !this.showShadow;
      this.setHeaderMarkup();
    }
  },
  watch: {
    heightVal: function () {
      if (this.heightVal < this.heightFloor) {
        this.heightVal = this.heightFloor;
      }

      this.setHeaderMarkup();
    },
    outputStyles: function () {
      this.setHeaderMarkup();
    }
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