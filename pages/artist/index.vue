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
            <nuxt-link to="/artist/create"
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
            <tr v-for="item in desserts" :key="item.name">
              <td>{{ item.name }}</td>
              <td>{{ item.calories }}</td>
              <td></td>
              <td></td>
              <td><v-btn color="warning">แก้ไข</v-btn></td>
              <td><v-btn color="error">ลบ</v-btn></td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data() {
    return {
      desserts: [
        {
          name: "The Toy",
          calories: "The Toy"
        },
        {
          name: "Black Pink",
          calories: "Black Pink"
        },
        {
          name: "BTS",
          calories: "BTS"
        }
      ]
    };
  }
};
</script>
