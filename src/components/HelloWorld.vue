<template>
  <div class="hello">
    <div>
      <b-form inline>
        <label class="sr-only" for="inline-form-input-name">Search Query</label>
        <b-form-input
          id="inline-form-input-name"
          class="mb-2 mr-sm-2 mb-sm-0"
          placeholder="Jane Doe"
          v-model="query"
        ></b-form-input>

        <b-button variant="primary" @click="getData">Search</b-button>
      </b-form>
    </div>
    <div v-if="condition === true">
      <b-card tag="article" style="max-width: 20rem" class="mb-2">
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
