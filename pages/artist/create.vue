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
            <nuxt-link to="/artist"
              ><v-btn color="warning">ย้อนกลับ</v-btn></nuxt-link
            >
          </v-col>
        </v-row>
      </v-container>
      <v-card class="pa-10">
        <v-form ref="form" v-model="valid" :lazy-validation="lazy">
          <v-text-field
            label="Solo"
            placeholder="ชื่อศิลปิน"
            solo
          ></v-text-field>
          <v-select :items="items" label="ประเภทศิลปิน" solo></v-select>
          <v-menu
            ref="menu"
            v-model="menu"
            :close-on-content-click="false"
            :return-value.sync="date"
            transition="scale-transition"
            offset-y
            min-width="290px"
          >
            <template v-slot:activator="{ on }">
              <v-text-field
                v-model="date"
                label="วันเกิดศิลปิน"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker v-model="date" no-title scrollable>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="menu = false">Cancel</v-btn>
              <v-btn text color="primary" @click="$refs.menu.save(date)"
                >OK</v-btn
              >
            </v-date-picker>
          </v-menu>
          <v-file-input
            label="รูปศิลปิน"
            filled
            prepend-icon="mdi-camera"
          ></v-file-input>
          <v-btn color="success" block>ยืนยัน</v-btn>
        </v-form>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data: () => ({
    items: ["Foo", "Bar", "Fizz", "Buzz"]
  })
};
</script>
