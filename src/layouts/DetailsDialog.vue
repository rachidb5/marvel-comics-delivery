<template>
  <v-container class="fill-height">
    <v-responsive class="d-flex align-center text-center fill-height">
      <v-row>
        <v-btn class="m-5">Ver detalhes</v-btn>
        <v-btn class="m-5">Solicitar entrega</v-btn>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "User",
  data() {
    return {
      comics: {},
    };
  },
  created() {
    this.getComics();
    console.log(this.comics);
  },
  methods: {
    getComics() {
      axios
        .get(
          "http://gateway.marvel.com/v1/public/comics?ts=1&apikey=2640839b89de352c4d01bd80b90c95e4&hash=62860b4c147756bf75696318c158704b"
        )
        .then((res) => {
          this.comics = res.data.data.results;
          console.log(this.comics);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
//  http://gateway.marvel.com/v1/public/comics?ts=1&apikey=2640839b89de352c4d01bd80b90c95e4&hash=62860b4c147756bf75696318c158704b
</script>
