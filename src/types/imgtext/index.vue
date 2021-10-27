<template>
  <!-- Directus File Interface needs to go here -->
  <interface-file-image v-model="imgtext.img"></interface-file-image>
  <QuillEditor
    theme="snow"
    v-model:content="modtext"
    contentType="html"
    :toolbar="customToolbar"
    @update:content="updateProp($event)"
  />
</template>

<script lang="ts">
import { QuillEditor } from "@vueup/vue-quill";
import "@vueup/vue-quill/dist/vue-quill.snow.css";

export default {
  props: {
    imgtext: {
      type: Object,
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
    updateProp(val) {
      console.log(val);
      this.$emit("update:imgtext", { txt: val });
    },
    updateImage(val) {
      console.log(val);
      this.$emit("update:imgtext", { img: val });
    },
  },
  components: {
    QuillEditor,
  },
};
</script>