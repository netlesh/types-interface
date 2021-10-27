<template>
  <interface-file-image
    @input="updateImage($event)"
    v-model:input="imgtext.imageID"
  ></interface-file-image>
  <QuillEditor
    theme="snow"
    v-model:content="imgtext.html"
    contentType="html"
    :toolbar="customToolbar"
    @update:content="updateHtml($event)"
  />
</template>

<script lang="ts">
import { QuillEditor } from "@vueup/vue-quill";
import "@vueup/vue-quill/dist/vue-quill.snow.css";

export default {
  props: {
    imgtext: {
      type: Object,
      default() {
        return {
          imageID: "",
          html: "",
        };
      },
    },
  },

  emits: ["update:imgtext"],
  data() {
    return {
      customToolbar: [
        [{ header: [2, 3, false] }],
        ["bold", "italic", "underline"],
        [{ list: "ordered" }, { list: "bullet" }],
      ],
    };
  },
  methods: {
    updateHtml(h) {
      console.log("htmlData changed" + h);
      this.$emit("update:imgtext", { html: h });
    },
    updateImage(id) {
      console.log("imageID changed:" + id);
      this.$emit("update:imgtext", { imageID: id });
    },
  },
  components: {
    QuillEditor,
  },
  mounted() {
    console.log("this.$props.imgtext :>> ", this.$props.imgtext);
  },
};
</script>