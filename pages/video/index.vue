<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
      <v-container>
        <v-row>
          <v-col>
            <h1>Artist Management</h1>
          </v-col>
          <v-spacer></v-spacer>
          <v-col class="text-right">
            <nuxt-link to="/artist/create" style="text-decoration:none;"
              ><v-btn color="success">สร้าง</v-btn></nuxt-link
            >
          </v-col>
        </v-row>
      </v-container>
      <v-simple-table>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">รูปภาพ</th>
              <th class="text-left">ชื่อศิลปิน</th>
              <th class="text-left">วันเกิด</th>
              <th class="text-left">ประเภทศิลปิน</th>
              <th class="text-left">แก้ไข</th>
              <th class="text-left">ลบ</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in artistLists" :key="item.id">
              <td>
                <img
                  class="artist_img"
                  :src="item.image_url"
                  alt="artist_img"
                />
              </td>
              <td>{{ item.name }}</td>
              <td></td>
              <td>{{ item.type }}</td>
              <td>
                <v-btn :to="'/artist/' + item.id + '/edit'" color="warning"
                  >แก้ไข</v-btn
                >
              </td>
              <td>
                <v-btn color="error" @click="deleteArtist(item.id)">ลบ</v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
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
    this.getArtistList();
  },
  data() {
    return {
      artistLists: {
        name: ""
      }
    };
  },
  methods: {
    getArtistList() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/get_artist",
          {
            limit: 100
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
            this.artistLists = response.data.data;
          }
        });
    },
    deleteArtist(myid) {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/delete_artist_by_artist_id",
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
          if(response.data.code == 0) {
            this.getArtistList();
          }
        });
    }
  }
};
</script>
