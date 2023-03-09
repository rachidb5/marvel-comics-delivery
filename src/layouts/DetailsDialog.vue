<template>
  <div>
    <v-card-title style="word-break: normal;">{{ comic.title }}</v-card-title>
    <v-card-subtitle>$ {{ price.price }}</v-card-subtitle>
    <v-row>
      <v-col>
        <v-card-text>{{ description.text }}</v-card-text>
      </v-col>
      <v-col>
        <v-img
          v-if="comic.thumbnail"
          :src="`${comic.thumbnail.path}/portrait_incredible.${comic.thumbnail.extension}`"
          height="250px"
          class="white--text align-end mt-2 mb-2"
        />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from "axios";

export default {
  setup() {},
  props: {
    comicId: { type: Number, required: true },
  },
  data() {
    return {
      comic: {},
      dialog: false,
      price: 0,
      description: "",
    };
  },
  created() {
    this.getComicById();
  },
  methods: {
    getComicById() {
      axios
        .get(
          `http://gateway.marvel.com/v1/public/comics/${this.comicId}?ts=1&apikey=2640839b89de352c4d01bd80b90c95e4&hash=62860b4c147756bf75696318c158704b`
        )
        .then((res) => {
          this.comic = res.data.data.results[0];
          this.price = res.data.data.results[0].prices[0];
          if(res.data.data.results[0].textObjects.length > 0){
            this.description = res.data.data.results[0].textObjects[0];
          }
          console.log(this.comic);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
//  http://gateway.marvel.com/v1/public/comics?ts=1&apikey=2640839b89de352c4d01bd80b90c95e4&hash=62860b4c147756bf75696318c158704b
//`http://gateway.marvel.com/v1/public/comics/${this.comicId}?ts=1&apikey=2640839b89de352c4d01bd80b90c95e4&hash=62860b4c147756bf75696318c158704b`
</script>
