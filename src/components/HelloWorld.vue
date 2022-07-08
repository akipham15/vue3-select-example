<template>
  <div>
    <h1>Vue Select</h1>
    <v-select
      :options="options"
      multiple
      label="text"
      @search="fetchOptions"
      v-model="selected"
      class="select-component"
    ></v-select>
    {{selected}}
  </div>
</template>

<script>
import vSelect from "vue-select";
import "vue-select/dist/vue-select.css";

export default {
  components: {
    "v-select": vSelect,
  },
  data() {
    return {
      options: ["foo", "bar", "baz"],
      selected: [],
    };
  },
  methods: {
    getPost(search, vm) {
      fetch(`https://jsonplaceholder.typicode.com/posts?q=${search}`)
        .then((response) => response.json())
        .then((data) => {
          let results = data.map((x) => {
            return { id: x.id, text: x.title };
          });
          vm.options = results;
        });
    },
    fetchOptions(search, loading) {
      loading(false);
      if (search.length) {
        this.getPost(search, this);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.select-component {
  margin: auto;
  max-width: 20%;
  background-color: white;
  margin-top: -5px;
}
</style>
