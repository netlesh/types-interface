<template>
  <interface-file-image @input="setImageIDProp($event)"></interface-file-image>
  <h3>ID: {{ imageID }}</h3>
</template>

<script lang="ts">
export default {
  props: {
    imageID: {
      type: String,
      default: "a6d8db95-fdce-4c7b-b92d-257a59d2a5ca",
    },
  },
  emits: ["update.imageID"],
  methods: {
    setImageIDProp(id) {
      this.$props.imageID = id;
      console.log(this.imageID);
      this.$emit("update.imageID", id);
    },
  },
};
</script>
<style lang="scss" scoped>
h3 {
  margin-top: 1rem;
}
</style>