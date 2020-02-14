<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
      <v-container>
        <v-row>
          <v-col>
            <h1>Video Management</h1>
          </v-col>
          <v-spacer></v-spacer>
          <v-col class="text-right">
            <nuxt-link to="/video/create" style="text-decoration:none;">
              <v-btn color="success">สร้าง</v-btn>
            </nuxt-link>
          </v-col>
        </v-row>
      </v-container>
      <v-simple-table>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">รูปภาพ</th>
              <th class="text-left">ชื่อวิดีโอ</th>
              <th class="text-left">ชื่อศิลปิน</th>
              <th class="text-left">วิว</th>
              <th class="text-left">แก้ไข</th>
              <th class="text-left">ลบ</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in videoLists" :key="item.id">
              <td>
                <img class="artist_img" :src="item.image_url" alt="video_img" />
              </td>
              <td>{{ item.title }}</td>
              <td>{{ item.artist_name }}</td>
              <td>{{ item.views }}</td>
              <td>
                <v-btn :to="'/video/' + item.id + '/edit'" color="warning"
                  >แก้ไข</v-btn
                >
              </td>
              <td>
                <v-btn color="error" @click="deleteVideo(item.id)">ลบ</v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
      <div class="text-right ma-2">
        <v-btn @click="previousPage()" color="dark">
          <v-icon>mdi-arrow-left-thick</v-icon>
        </v-btn>
        <v-btn @click="nextPage()" color="dark">
          <v-icon>mdi-arrow-right-thick</v-icon>
        </v-btn>
      </div>
    </v-flex>
  </v-layout>
</template>

<style scoped>
.artist_img {
  width: 200px;
  height: 200px;
  object-fit: cover;
}
</style>

<script>
import axios from "axios";
export default {
  mounted() {
    this.getVideoList();
  },
  data() {
    return {
      videoLists: {}
    };
  },
  methods: {
    previousPage() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/get_video",
          {
            limit: 10,
            last_id: this.videoLists[1].id,
            order: "desc"
          },
          {
            headers: {
              "Content-type": "application/json",
              Authorization: "Basic YWlzc3RhcmJvb3N0ZXI6Ym9vc3RlcmFpc0AyMDE5"
            }
          }
        )
        .then(response => {
          this.videoLists = response.data.data;
        });
    },
    nextPage() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/get_video",
          {
            limit: 10,
            last_id: this.videoLists[9].id
          },
          {
            headers: {
              "Content-type": "application/json",
              Authorization: "Basic YWlzc3RhcmJvb3N0ZXI6Ym9vc3RlcmFpc0AyMDE5"
            }
          }
        )
        .then(response => {
          this.videoLists = response.data.data;
        });
    },
    getVideoList() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/get_video",
          {
            limit: 10
          },
          {
            headers: {
              "Content-type": "application/json",
              Authorization: "Basic YWlzc3RhcmJvb3N0ZXI6Ym9vc3RlcmFpc0AyMDE5"
            }
          }
        )
        .then(response => {
          if (response.data.code == 0) {
            this.videoLists = response.data.data;
          }
        });
    },
    deleteVideo(myid) {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/delete_video_by_video_id",
          {
            id: myid
          },
          {
            headers: {
              "Content-type": "application/json",
              Authorization: "Basic YWlzc3RhcmJvb3N0ZXI6Ym9vc3RlcmFpc0AyMDE5"
            }
          }
        )
        .then(response => {
          if (response.data.code == 0) {
            this.getVideoList();
          }
        });
    }
  }
};
</script>
