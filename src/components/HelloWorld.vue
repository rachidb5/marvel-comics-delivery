<template>
  <v-container class="fill-height">
    <v-responsive class="d-flex align-center text-center fill-height">
      <DetailsDialog />
      <v-row>
        <v-col v-for="c in comics" cols="4">
          <v-card class="p-3">
            <v-card-title>{{ c.title }}</v-card-title>
            <v-img
              :src="`${c.thumbnail.path}/portrait_incredible.${c.thumbnail.extension}`"
              height="200px"
              class="white--text align-end mt-2 mb-2"
            />
            <div
              class="d-flex justify-space-around align-center flex-column flex-md-row fill-height mb-4"
            >
              <v-btn class="m-5" color="white" variant="outlined">Ver detalhes</v-btn>
              <v-btn class="m-5" color="#ed1d24">Solicitar entrega</v-btn>
            </div>
          </v-card>
        </v-col>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script>
import axios from "axios";
import DetailsDialog from '@/layouts/DetailsDialog.vue'

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
