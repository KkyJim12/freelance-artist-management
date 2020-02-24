<template>
  <dropzone
    id="foo"
    ref="el"
    :options="options"
    :destroyDropzone="true"
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
      // See https://rowanwins.github.io/vue-dropzone/docs/dist/index.html#/props
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
  mounted() {
    // Everything is mounted and you can access the dropzone instance
    const instance = this.$refs.el.dropzone;
  }
};
</script>
