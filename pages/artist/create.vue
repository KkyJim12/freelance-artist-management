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
            placeholder="ชื่อศิลปิน"
            v-model="artist_name"
            solo
          ></v-text-field>
          <v-text-field
            placeholder="บูส"
            type="number"
            solo
            v-model="boosts"
          ></v-text-field>
          <v-text-field
            placeholder="คีย์เวิร์ด"
            type="text"
            v-model="keywords"
            solo
          ></v-text-field>
          <v-text-field
            placeholder="mission"
            type="text"
            v-model="mission"
            solo
          ></v-text-field>
          <v-text-field
            placeholder="ชื่อ"
            type="text"
            v-model="name"
            solo
          ></v-text-field>
          <label>รูปหลัก</label>
          <image-upload></image-upload>
          <label>รูปโปสเตอร์</label>
          <image-upload></image-upload>
          <v-btn class="mt-5" @click="addArtist()" color="success" block>ยืนยัน</v-btn>
        </v-form>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
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
    addArtist() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/add_artist",
          {
            artist_name: this.artist_name,
            boost: this.boost,
            enabled: this.enabled,
            image_url: this.image_url,
            keywords: this.keywords.split(","),
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
          console.log(response.data.code);
          if (response.data.code == 0) {
            this.$router.push("/artist");
          }
        });
    }
  }
};
</script>
