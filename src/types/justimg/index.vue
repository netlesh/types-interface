<template>
  <interface-file-image @input="getImageID($event)"></interface-file-image>
</template>

<script lang="ts">
export default {
  methods: {
    getImageID(id: string) {
      console.log("id:>> ", id);
    },
  },
};
</script>
