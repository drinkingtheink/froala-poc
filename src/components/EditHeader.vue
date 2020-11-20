<template>
  <section>
    <h3>Edit Your Header</h3>

    <section class="section-toolbar">
      <div class="set-section set-height">
        <label for="heightVal">Height:</label>
        <input 
          id="heightVal" 
          type="number" 
          v-model="heightVal" 
        />
        <span>px</span>
      </div>

      <div class="set-section set-shadow">
        <label for="dropShadow">Shadow:</label>
        <button 
          id="dropShadow" 
          class="radio" 
          v-on:click="toggleShadow"
          v-on:submit="toggleShadow"
        >
          <span v-if="showShadow">Turn Off Shadow</span>
          <span v-else>Show Shadow</span>
        </button>
      </div>

      <div class="set-section set-shadow">
        <label for="dropShadow">Header BG Color:</label>
        
        <section class="color-options bg-color-options">
          <button
            class="single-color-option"
            v-bind:class="[backgroundColor === color.val ? 'active' : '']"
            v-for="color in colorOptions"
            v-on:click="setBgColor(color.val)"
            v-on:submit="setBgColor(color.val)"
            v-bind:style="{ backgroundColor: `${color.val}` }"
          >
          </button>
        </section>
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
  props: ['colorOptions'],
  data () {
    return {
      heightVal: 50,
      heightFloor: 40,
      backgroundColor: '#333333',
      imgSrc: '/assets/okta-logo.png',
      publicPath: process.env.BASE_URL,
      headerMarkup: null,
      showShadow: true,
    }
  },
  computed: {
    outputStyles() {
      let styleBlock = {
        height: `${this.heightVal}px`,
        backgroundColor: `${this.backgroundColor}`,
        boxShadow: this.dropShadowStyles

      }
      return styleBlock;
    },
    dropShadowStyles() {
      let shadowStyles = `1px 5px 6px 1px rgba(0,0,0,0.37)`
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
    },
    setBgColor(color) {
      this.backgroundColor = color;
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
  border: 4px solid rgba(0,0,0,0.25);
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

.section-toolbar {
  display: flex;
  justify-content: center;

  .set-section {
    padding: 0 1rem;
  }

  label {
    display: block;
  }

  input {
    font-size: 1rem;
    margin-right: .25rem;
  }

  #heightVal {
    width: 2.5rem;
  }

  #dropShadow {
    width: 10rem;
  }

  .color-options {
    .single-color-option {
      padding: 1rem;
      border-radius: 20px;
      margin-right: .25rem;
      border: 4px solid rgba(0,0,0,0.25);

      &:hover {
        cursor: pointer;
      }

      &.active {
        border-color: red;
      }
    }
  }
}
</style>