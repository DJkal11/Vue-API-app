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

        <!-- <h1 v-for="item in data" :key="item">
          {{ item }}
        </h1> -->

        <b-button variant="primary" @click="getData">Search</b-button>
      </b-form>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  query = "";

  async getData() {
    const options = {
      method: "POST",
      headers: {},
      body: JSON.stringify({ page: 0, perPage: 15, searchQuery: this.query }),
    };

    const response = await fetch(
      "https://org.bapi.devcurate.co/api/JobBoard/search",
      options
    );
    const data = response.json;
    console.log(data);

    if (data) {
      return data;
    } else {
      return "";
    }
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
