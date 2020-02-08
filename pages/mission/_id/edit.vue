<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
      <v-container>
        <v-row>
          <v-col>
            <h1>Mission Management Edit</h1>
          </v-col>
          <v-spacer></v-spacer>
          <v-col class="text-right">
            <nuxt-link to="/mission" style="text-decoration:none;">
              <v-btn color="warning">ย้อนกลับ</v-btn>
            </nuxt-link>
          </v-col>
        </v-row>
      </v-container>
      <v-card class="pa-10">
        <v-form ref="form">
          <v-text-field label="Solo" placeholder="id ศิลปิน" solo v-model="artist_id"></v-text-field>
          <v-text-field label="Solo" placeholder="บูส" type="number" solo v-model="boosts"></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="บูสที่ต้องใช้"
            type="number"
            solo
            v-model="boosts_need"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="id หมวดหมู่"
            type="number"
            solo
            v-model="category_id"
          ></v-text-field>
          <v-text-field label="Solo" placeholder="ลิงค์รูป" type="text" solo v-model="image_url"></v-text-field>
          <v-text-field label="Solo" placeholder="mission" type="text" solo v-model="mission"></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="mission_desc"
            type="text"
            solo
            v-model="mission_desc"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="mission_end"
            type="text"
            solo
            v-model="mission_end"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="mission รูป"
            type="text"
            solo
            v-model="mission_image_url"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="mission_start"
            type="text"
            solo
            v-model="mission_start"
          ></v-text-field>
          <v-text-field label="Solo" placeholder="ชื่อ" type="text" solo v-model="name"></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="ลิงค์รูปโปสเตอร์"
            type="text"
            solo
            v-model="poster_url"
          ></v-text-field>
          <v-btn @click="updateMission()" color="success" block>ยืนยัน</v-btn>
        </v-form>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from "axios";
export default {
  mounted() {
    this.getMissionInfo();
  },
  data() {
    return {
      artist_id: "",
      boosts: "",
      boosts_need: "",
      enabled: true,
      category_id: "",
      image_url: [],
      mission: "",
      mission_desc: "",
      mission_image_url: "",
      mission_start: "",
      mission_end: "",
      name: "",
      poster_url: ""
    };
  },
  methods: {
    getMissionInfo() {
      axios.post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/get_mission",
          {
            artist_id: this.artist_id,
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
            this.$router.push("/mission");
          }
        });
    },
    updateMission() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/update_mission_by_mission_id",
          {
            artist_id: this.artist_id,
            boosts: this.boosts,
            boosts_need: this.boosts_need,
            enabled: this.enabled,
            category_id: this.category_id,
            image_url: this.image_url,
            mission: this.mission,
            mission_desc: this.mission_desc,
            mission_image_url: this.mission_image_url,
            mission_start: this.mission_start,
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
            this.$router.push("/mission");
          }
        });
    }
  }
};
</script>
