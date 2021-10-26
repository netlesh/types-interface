<template>
  <interface-file-image @input="getImageID($event)"></interface-file-image>
  <h3>ID: {{ imageId }}</h3>
</template>

<script lang="ts">
export default {
  data() {
    return {
      imageId: "",
    };
  },
  methods: {
    getImageID(id) {
      this.imageId = id;
    },
  },
};
</script>
<style lang="scss" scoped>
h3 {
  margin-top: 1rem;
}
</style>