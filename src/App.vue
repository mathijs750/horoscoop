<template>
  <div class="grid-container">
    <div class="Title">
      <h1>De BSN Horoscoop</h1>
    </div>
    <div class="SearchArea">
      <div class="label-box">
        <input @input="onInput" v-model="bsn" type="number" placeholder="Uw BSN" number/>
      </div>
      <button @click="onSearch" :disabled="!isBSNValid">Zoek</button>
    </div>
    <div class="Result" v-if="hasValid">
      <h1>Lief {{ bsn }}tje,</h1>
      <hr>
      <p>
        In uw toekomst zie ik veel slechte keuzes. U zal veel rekeningen gaan zien op uw naam zonder dat u daar zelf iets voor hoeft te doen.
      </p>
      <p>
        Vul in het vervolg geen BSN's in op willekeurige websites.
      </p>
    </div>
    <div class="Result" v-if="hasInvalid">
      <h1>{{ bsn }}, hoe durf je?</h1>
      <p>
        Het Orakel is woest! Leugens zullen ernstige conequeties hebben in uw toekomst. Neem nu maar alvast afscheid van uw geliefden.
      </p>
      <p>
        Het Orakel neemt alleen geldige BSN's in behandeling.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  computed: {
    isBSNValid() {
      return this.bsn.length === 9
    }
  },
  data() {
    return {
      bsn: "",
      hasValid : false,
      hasInvalid : false
    };
  },
  methods: {
    onInput() {
      if (this.bsn.length > 9) {
        this.bsn = this.bsn.slice(0, 9);
      }
    },
    onSearch() {
      console.log("Dit is gelukkig alleen maar in je browser. 💖")

      let factor = 9
      let runningTotal = 0
      
      this.bsn.split('').forEach((element, index) => {
        if (index === 8) {
          runningTotal += -1 * element
        }
        else{
          runningTotal += factor * element
          factor--
        }
      });

      if (runningTotal % 11 === 0){
        this.hasValid = true
      }
      else {
        this.hasInvalid = true
      }
    }
  }
};
</script>

<style lang="scss">
$dark-color: #2c3e50;
$light-color: #ffffff;
$cta-color: rgb(255, 201, 51);
$cta-color-disabled: rgba(255, 216, 108, 0.568);
$light-background-color:  rgb(231, 255, 244);
$background-color: #265568;
$font: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;

html,
body {
  margin: 0;
  padding: 0;
  min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $light-color;
  background-color: $background-color;
  min-height: 100vh;

  background-image: url("./assets/bg3-min.jpg");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  
}

.grid-container {
  display: grid;
  grid-template-columns: 1fr minmax(min-content, 800px) 1fr;
  grid-template-rows: 20vh 1fr 1.2fr;
  gap: 0px 0px;
  min-height: 100vh;
}

h1, h2, h3{
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
    color: $light-color;
  }

.Title {
  grid-area: 1 / 2 / 2 / 3;
  display: flex;
  justify-self: center;
  align-items: center;

  h1{
    font-size: 3em;
  }
}

.SearchArea {
  grid-area: 2 / 2 / 3 / 3;
  
  // display:flex;
  // justify-content:space-around;
  padding: 1em;

  .label-box {
    max-width: 100%;
    //min-width: 70vw;
    padding: .5em;
    background-color: $light-background-color;

    input {
      position: relative;
      font-size: 2.5em;
      letter-spacing: .05em;
      color: $dark-color;
      font-family: $font;
      text-align: center;
      line-height: 3em;
      border-width: 3px;
      border-style: solid;
      border-color: $dark-color;
      background-color: $light-background-color;
      outline: none;
      width:100%;
      box-sizing: border-box;
      }
  }

  button{
    font-family: $font;
    background-color: $cta-color;
    border-color: $dark-color;
    font-size: 1.3em;
    padding: .2em;
    border-width: 3px;
    border-style: solid;
    color: $dark-color;
    border-color: $cta-color;
    background-color: $cta-color;
    margin-top: 1em;
    min-width: 30%;

    &:disabled{
      opacity:0.6;
      filter:grayscale(0.6)
    }
  }
}

hr {
  color: $light-color;
  max-width: 80%;
  margin: .3em auto;
}

p {
  margin: 1.5em auto;
}

.Result {
  grid-area: 3 / 2 / 4 / 3;
  background-color: $background-color;
  padding: 2em;

  h1{
    margin-top: 0.5em;
  }
}

/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
}
</style>
