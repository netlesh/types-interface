<template>
  <interface-file-image @input="getImageID($event)"></interface-file-image>
</template>

<script>
export default {
  methods: {
    getImageID(id) {
      console.log("id:>> ", id);
    },
  },
};
</script>
