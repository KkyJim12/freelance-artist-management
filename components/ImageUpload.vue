<template>
  <dropzone
    id="foo"
    ref="el"
    :options="options"
    @vdropzone-success="vsuccess"
  ></dropzone>
</template>
<script>
import Dropzone from "nuxt-dropzone";
import "nuxt-dropzone/dropzone.css";

export default {
  components: {
    Dropzone
  },
  data() {
    return {
      options: {
        url:
          "https://us-central1-star-booster-ais-new-bis.cloudfunctions.net/upload_image",
        thumbnailWidth: 150,
        maxFilesize: 2,
        maxFiles: 1,
        headers: {
          Authorization: "Basic YWlzc3RhcmJvb3N0ZXI6Ym9vc3RlcmFpc0AyMDE5"
        }
      }
    };
  },
  methods: {
    vsuccess: function(file, response) {
      this.$emit("image", response.data);
    }
  },
  mounted() {
    const instance = this.$refs.el.dropzone;
  }
};
</script>
