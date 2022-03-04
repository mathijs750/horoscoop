<template>
  <div class="grid-container">
    <div class="Title">
      <h1>De BSN Horoscoop</h1>
    </div>
    <div class="SearchArea">
      <div class="label-box">
        <label>
          <input @input="onInput" v-model="bsn" type="number" placeholder="Uw BSN"/>
        </label>
      </div>
      <button @click="onSearch" :disabled="!isBSNValid">Zoek</button>
    </div>
    <div class="Result" v-if="hasResult">
      <h1>{{ hasValid ? greetings.valid : greetings.invalid }} {{ bsn }},</h1>
      <hr />
      <p>{{ hasValid ? makePrediction() : expressDisappointment() }}</p>
      <p>{{ hasValid ? advice.valid : advice.invalid }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  computed: {
    isBSNValid() {
      return this.bsn.toString().length === 9;
    },
  },
  data() {
    return {
      bsn: "",
      hasValid: false,
      hasResult: false,
      predictions: [
        "In uw toekomst zie ik veel slechte keuzes. De Maan, uw belangrijkste planeet, en Uranus staan lijnrecht " +
          "tegenover elkaar. Wees daarom niet verbaast als er een nieuwe woonruimte op uw naam staat.",

        "Komend jaar kunt u beter niet een al te hoog eigen risico nemen. Er zullen namelijk veel rekeningen komen " +
          "van uw zorgverzekeraar. De slechte stand van Mars zal dit niet beter maken.",

        "De Maan en een onvoorspelbare Uranus gaan even wat minder goed door één deur, dat heeft gevolgen. " +
          "U moet op verhoor komen, omdat de politie u als verdachte zal zien.",

        "Jupiter staat goed, net als de nieuw leningen op uw naam. Hou er rekening mee dat U wordt aangehouden " +
          "bij een grensovergang.",

        "U ontvangt binnenkort boze berichten van mensen die u als oplichter zien. Mercurius is halverwege dus " +
          "blijf weg weg van  een online marktplaatsen.",
      ],
      disappointment: [
        "Het Orakel is woest! Leugens zullen ernstige conequeties hebben in uw toekomst. " +
          "Neem nu maar alvast afscheid van uw geliefden.",

        "Liegen is een slechte gewoonte. Uw dierbare praten daar vaak over achter uw rug om.",
      ],
      greetings: {
        valid: "Lieve",
        invalid: "Oh jee",
      },
      advice: {
        valid: "Vul in het vervolg geen BSN's in op willekeurige websites.",
        invalid: "Het Orakel neemt alleen geldige BSN's in behandeling.",
      },
    };
  },
  methods: {
    makePrediction() {
      return this.predictions[
        Math.floor(Math.random() * this.predictions.length)
      ];
    },
    expressDisappointment() {
      return this.disappointment[
        Math.floor(Math.random() * this.disappointment.length)
      ];
    },
    onInput() {
      if (this.bsn.toString().length > 9) {
        this.bsn = this.bsn.toString().slice(0, 9);
      }
      this.hasResult = false;
    },
    onSearch() {
      console.log("Dit is gelukkig alleen maar in je browser. 💖");

      let factor = 9;
      let runningTotal = 0;

      this.bsn
        .toString()
        .split("")
        .forEach((element, index) => {
          if (index === 8) {
            runningTotal += -1 * element;
          } else {
            runningTotal += factor * element;
            factor--;
          }
        });

      this.hasValid = runningTotal % 11 === 0;
      this.hasResult = true;
    },
  },
};
</script>

<style lang="scss">
$dark-color: #2f4255;
$light-color: #ffffff;
$cta-color: rgb(255, 200, 50);
$light-background-color: rgb(210, 255, 235);
$background-color: #265568;
$font: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;

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
  grid-template-columns: 1fr minmax(min-content, 600px) 1fr;
  grid-template-rows: 20vh minmax(min-content, 30vh) 1fr;
}

h1,
h2,
h3 {
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
  color: $light-color;
}

.Title {
  grid-area: 1 / 2 / 2 / 3;
  display: flex;
  justify-self: center;
  align-items: center;
  padding: 32px;

  h1 {
    font-size: 3em;
  }
}

.SearchArea {
  grid-area: 2 / 2 / 3 / 3;
  padding: 16px;

  .label-box {
    max-width: 100%;
    padding: 0.5em;
    background-color: $light-background-color;

    input {
      position: relative;
      font-size: 2.5em;
      letter-spacing: 0.05em;
      color: $dark-color;
      font-family: $font;
      text-align: center;
      line-height: 3em;
      border-width: 3px;
      border-style: solid;
      border-color: $dark-color;
      background-color: $light-background-color;
      outline: none;
      width: 100%;
      box-sizing: border-box;
    }
  }

  button {
    font-family: $font;
    color: $dark-color;
    background-color: $cta-color;
    font-size: 1.3em;
    padding: 8px;
    border: 0;
    margin-top: 25px;
    min-width: 30%;

    &:disabled {
      opacity: 0.6;
      filter: grayscale(0.6);
    }
  }
}


hr {
  color: $light-color;
  max-width: 80%;
  margin: 8px auto;
}

p {
  margin: 1.5em auto;
  max-width: 52ch;
}

.Result {
  grid-area: 3 / 2 / 4 / 3;
  background-color: $background-color;
  padding: 32px;
  margin: 16px;

  h1 {
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
input[type="number"] {
  -moz-appearance: textfield;
}
</style>
