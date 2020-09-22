<template>
  <div>
    <v-toolbar
      dark
      prominent
      src="https://picsum.photos/1920/1080?random"
    >
      <v-toolbar-title style="font-size: 40px;">Vending Machine </v-toolbar-title>
    </v-toolbar>
    <VendingMachine />
  </div>
</template>

<script>
// @ is an alias to /src
import VendingMachine from "../components/VendingMachine";
export default {
  name: "Home",
  components: {
    VendingMachine,
  },
  mounted() {
    this.fetch();
  },
  methods: {
    fetch() {
      this.axios
        .get("v2/5c77c5b330000051009d64c9")
        .then((response) => {
          // console.log(response.data);
        })
        .catch((err) => {
          console.log(err.response);
        });
    },
  },
};
</script>

<style scoped>
.v-toolbar--prominent:not(.v-toolbar--bottom) .v-toolbar__title {
    align-self: flex-end;
    padding-bottom: 6px;
    padding-top: 0;
    margin-bottom: 2%;
}
</style>