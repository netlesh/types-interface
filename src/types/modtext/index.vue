<template>
  <QuillEditor
    theme="snow"
    v-model:content="modtext"
    contentType="html"
    :toolbar="customToolbar"
    @update:content="updateProp($event)"
  />
</template>

<script>
import { QuillEditor } from "@vueup/vue-quill";
import "@vueup/vue-quill/dist/vue-quill.snow.css";

export default {
  props: {
    modtext: {
      type: String,
      default: "",
    },
  },
  emits: ['update:modtext'],
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
          console.log(val)
          this.$emit('update:modtext', val)
      }
  },
  components: {
    QuillEditor,
  },
};
</script>