<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
      <v-container>
        <v-row>
          <v-col>
            <h1>Mission Management</h1>
          </v-col>
          <v-spacer></v-spacer>
          <v-col class="text-right">
            <nuxt-link to="/mission/create" style="text-decoration:none;">
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
              <th class="text-left">ขื่อ mission</th>
              <th class="text-left">ชื่อศิลปิน</th>
              <th class="text-left">แก้ไข</th>
              <th class="text-left">ลบ</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in missionLists" :key="item.id">
              <td>
                <img class="artist_img" :src="item.image_url" alt="artist_img" />
              </td>
              <td>{{ item.mission }}</td>
              <td>{{ item.artist_id }}</td>
              <td>
                <v-btn :to="'/mission/' + item.mission_id + '/edit'" color="warning">แก้ไข</v-btn>
              </td>
              <td>
                <v-btn color="error" @click="deleteMission(item.mission_id)">ลบ</v-btn>
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
    this.getMissionList();
  },
  data() {
    return {
      missionLists: {}
    };
  },
  methods: {
    getMissionList() {
      axios
        .post(
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/get_mission",
          {
            limit: 100,
            last_id: 2,
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
          if (response.data.code == 0) {
            this.missionLists = response.data.data;
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
          if (response.data.code == 0) {
            this.getArtistList();
          }
        });
    }
  }
};
</script>
