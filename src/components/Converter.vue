<template>
  <section class="container">
    <header class="converter__header">
      <h2 class="converter__text--title">
        Conversor de <span class="converter__text--focus">{{ from }}</span> para
        <span class="converter__text--focus">{{ to }}</span>
      </h2>
    </header>

    <main class="converter__main">
      <form class="form">
        <div class="form__group">
          <label class="form__label" for="valor">Valor</label>
          <input
            type="number"
            name="valor"
            class="form__input"
            v-model="valueConvert"
            :placeholder="'Valor da moeda ' + from"
          />
        </div>
        <button type="submit" class="form__btn" @click.prevent="convert">
          Converter
        </button>
      </form>
    </main>

    <p v-if="result.value" class="converter__text">
      Resultado da conversão é:
      <span class="converter__text--focus converter__text--outline">{{
        resultFmt
      }}</span>
    </p>
  </section>
</template>

<script>
export default {
  name: "converter",
  data: () => ({ valueConvert: null, result: { value: undefined } }),
  props: {
    from: {
      default: "BRL",
    },
    to: {
      default: "USD",
    },
  },
  watch: {
    // // result: [
    // //   "watchResult",
    // //   function () {
    // //     console.log("watch função");
    // //   },
    // // ],

    // result(value) {
    //   console.log("Watch metódo");
    //   console.log("Valor Antigo", this.result.value);
    //   console.log("Novo Valor", value.value);
    // },

    result: {
      handler() {
        console.log("Watch em uma unica propriedade");
      },
      deep: true,
    },
  },
  computed: {
    resultFmt() {
      console.log("resultFmt");
      return new Intl.NumberFormat("pt-BR", {
        style: "currency",
        currency: this.to,
      }).format(this.result.value);
    },
  },
  methods: {
    async convert() {
      this.$nextTick;
      if (this.valueConvert) {
        const url = `https://free.currconv.com/api/v7/convert?q=${this.from}_${this.to}&compact=ultra&apiKey=75ff32c7841aeb5bd3f3`;
        const request = await fetch(url);
        const response = await request.json();

        const result = response[`${this.from}_${this.to}`];

        if (result) {
          if (this.result) {
            this.result = {
              value: result * this.valueConvert,
            };
          } else {
            this.result.value = result * this.valueConvert;
          }
        }
      }
    },
    watchResult(value) {
      console.log("Watch metódo");
      console.log("Valor Antigo", this.result.value);
      console.log("Novo Valor", value.value);
    },
    resultFmtMethod() {
      console.log("resultFmtMethod");
      return new Intl.NumberFormat("pt-BR", {
        style: "currency",
        currency: this.to,
      }).format(this.result.value);
    },
  },
};
</script>

<style lang="sass" scoped>
.container
    display: flex
    flex-direction: column
    width: fit-content
    padding: 15px
    background: #d3cfcf5e
    border-radius: 6px
    box-shadow: 6px 7px 11px -5px rgba(71,71,71,0.56)
    height: 205px

.converter
    &__header
        margin-bottom: 15px

    &__text
        font-weight: 300
        &--title
            font-weight: 300
        &--focus
            font-weight: 400
        &--outline
            display: block
            margin: 0 10px

    &__main
        display: flex
        flex-direction: column

.form
    margin-bottom: 15px
    &__group
        margin-bottom: 15px
        display: flex
        flex-direction: column

    &__input
        margin: 0 10px
        background: none
        border: none
        border-bottom: 1px solid
        outline: none

    &__btn
        background: none
        border: none
        outline: none
        font-weight: bold
</style>