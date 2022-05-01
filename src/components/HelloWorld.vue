<template>
  <div class="hello">
    <div class="input">
      <b-form inline>
        <label class="sr-only input-label" for="inline-form-input-name"
          >Search Query</label
        >
        <b-form-input
          id="inline-form-input-name"
          class="input-text"
          placeholder="Jane Doe"
          v-model="query"
        ></b-form-input>

        <b-button variant="primary" @click="getData">Search</b-button>
      </b-form>
    </div>
    <div class="response" v-if="condition === true">
      <b-card tag="article" style="max-width: 20rem" class="mb-2 card">
        <h1>{{ query }}</h1>
        <b-card-text>
          <b>Abilities</b>
        </b-card-text>
        <b-card-text>
          {{ answer.abilities[0].ability.name }}
        </b-card-text>
        <b-card-text>
          <b>Type</b>
        </b-card-text>
        <b-card-text>
          {{ answer.types[0].type.name }}
        </b-card-text>
      </b-card>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  query: any;
  answer = "";
  condition = false;

  async getData() {
    const options = {
      method: "GET",
      headers: {},
    };

    const response = await fetch(
      "https://pokeapi.co/api/v2/pokemon/" + this.query + "/",
      options
    ).then((res) => res.json());
    this.condition = true;
    this.answer = response;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input {
  margin: auto;
  margin-top: 10em;
  background-color: rgb(255, 71, 209);
  opacity: 0.8;
  width: 20em;
  height: 20em;
  padding-top: 4em;
  border-radius: 50px;
  color: white;
}

.input-text {
  width: 15em;
  margin: auto;
  margin-bottom: 1em;
  margin-top: 1em;
}

.input-label {
  font-size: 2em;
}

.response {
  margin: auto;
  margin-top: 1em;
  width: 20em;
  height: 20em;
  padding-top: 4em;
  border-radius: 50px;
}

.card {
  background-color: rgb(71, 255, 191);
  opacity: 0.8;
  border-radius: 50px;
}
</style>
