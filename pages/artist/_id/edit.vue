<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
      <v-container>
        <v-row>
          <v-col>
            <h1>Artist Management Create</h1>
          </v-col>
          <v-spacer></v-spacer>
          <v-col class="text-right">
            <nuxt-link to="/artist" style="text-decoration:none;"
              ><v-btn color="warning">ย้อนกลับ</v-btn></nuxt-link
            >
          </v-col>
        </v-row>
      </v-container>
      <v-card class="pa-10">
        <v-form ref="form">
          <v-text-field
            label="Solo"
            placeholder="ชื่อศิลปิน"
            solo
            v-model="artist_name"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="บูส"
            type="number"
            solo
            v-model="boosts"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="ลิงค์รูป"
            type="text"
            solo
            v-model="image_url"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="คีย์เวิร์ด"
            type="text"
            solo
            v-model="keywords"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="mission"
            type="text"
            solo
            v-model="mission"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="ชื่อ"
            type="text"
            solo
            v-model="name"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="ลิงค์รูปโปสเตอร์"
            type="text"
            solo
            v-model="poster_url"
          ></v-text-field>
          <v-btn @click="updateArtist()" color="success" block>ยืนยัน</v-btn>
        </v-form>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from "axios";
export default {
  mounted() {
    this.getArtistById();
  },
  data() {
    return {
      id: "",
      artist_name: "",
      boosts: "",
      enabled: true,
      image_url: "",
      keywords: [],
      mission: "",
      name: "",
      poster_url: ""
    };
  },
  methods: {
    getArtistById() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/get_artist",
          {
            limit: 1,
            last_id: parseInt(this.$route.params.id)
          },
          {
            headers: {
              "Content-type": "application/json",
              Authorization: "Basic YWlzc3RhcmJvb3N0ZXI6Ym9vc3RlcmFpc0AyMDE5"
            }
          }
        )
        .then(response => {
          this.id = response.data.data[0].id;
          this.artist_name = response.data.data[0].artist_name;
          this.boosts = response.data.data[0].boosts;
          this.image_url = response.data.data[0].image_url;
          this.keywords = response.data.data[0].keywords;
          this.mission = response.data.data[0].mission;
          this.name = response.data.data[0].name;
          this.poster_url = response.data.data[0].poster_url;
        });
    },
    updateArtist() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/update_artist_by_artist_id",
          {
            id: this.id,
            artist_name: this.artist_name,
            boost: this.boost,
            enabled: this.enabled,
            image_url: this.image_url,
            keywords: this.keywords,
            mission: this.mission,
            name: this.name,
            poster_url: this.poster_url
          },
          {
            headers: {
              "Content-type": "application/json",
              Authorization: "Basic YWlzc3RhcmJvb3N0ZXI6Ym9vc3RlcmFpc0AyMDE5"
            }
          }
        )
        .then(response => {
          console.log(response.data);
        });
    }
  }
};
</script>
