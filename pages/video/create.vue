<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
      <v-container>
        <v-row>
          <v-col>
            <h1>Video Management Create</h1>
          </v-col>
          <v-spacer></v-spacer>
          <v-col class="text-right">
            <nuxt-link to="/video" style="text-decoration:none;"
              ><v-btn color="warning">ย้อนกลับ</v-btn></nuxt-link
            >
          </v-col>
        </v-row>
      </v-container>
      <v-card class="pa-10">
        <v-form ref="form">
          <v-select
            item-value="id"
            item-text="artist_name"
            :items="artistLists"
            label="ศิลปิน"
            v-model="artist_id"
            solo
          ></v-select>
          <v-text-field
            label="Solo"
            placeholder="ชื่อศิลปิน"
            solo
            type="number"
            v-model="artist_name"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="คอมเมนท์"
            solo
            type="number"
            v-model="comments"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="หัวข้อ"
            type="text"
            solo
            v-model="title"
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
            placeholder="ลิงค์ video"
            type="text"
            solo
            v-model="video_url"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="ประเภท video"
            type="text"
            solo
            v-model="video_type"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="วิว"
            type="number"
            solo
            v-model="views"
          ></v-text-field>
          <v-text-field
            label="Solo"
            placeholder="เริ่ม"
            type="date"
            solo
            v-model="start"
          ></v-text-field>
          <label>รูปหลัก</label>
          <image-upload @image="MainImageUpload"></image-upload>
          <label>รูป ศิลปิน</label>
          <image-upload @image="ArtistImageUpload"></image-upload>
          <v-btn class="mt-5" @click="addVideo()" color="success" block>ยืนยัน</v-btn>
        </v-form>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from "axios";
export default {
  mounted() {
    this.getArtistList();
  },
  data() {
    return {
      artist_id: "",
      artist_image_url: "",
      artist_name: "",
      comments: "",
      desc: "desc",
      enabled: false,
      is_highlight: false,
      is_live: false,
      image_url: "",
      keywords: [],
      start: "",
      title: "",
      video_url: "",
      video_type: "",
      views: "",
      artistLists: []
    };
  },
  methods: {
    MainImageUpload(image) {
      this.image_url = image;
    },
    ArtistImageUpload(image) {
      this.artist_image_url = image;
    },
    getArtistList() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/get_artist",
          "",
          {
            headers: {
              "Content-type": "application/json",
              Authorization: "Basic YWlzc3RhcmJvb3N0ZXI6Ym9vc3RlcmFpc0AyMDE5"
            }
          }
        )
        .then(response => {
          if (response.data.code == 0) {
            this.artistLists = response.data.data;
          }
        });
    },
    addVideo() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/add_video",
          {
            artist_id: this.artist_id,
            artist_image_url: this.artist_image_url,
            artist_name: this.artist_name,
            comments: this.comments,
            desc: this.desc,
            enabled: this.enabled,
            is_highlight: this.is_highlight,
            keywords: this.keywords.split(","),
            is_live: this.is_live,
            image_url: this.image_url,
            start: this.start,
            title: this.title,
            video_url: this.video_url,
            video_type: this.video_type,
            views: this.views
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
