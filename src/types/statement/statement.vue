<template>
  <div class="rightanswer">
    <h3>Aussagen angeben und korrekte Antwort markieren:</h3>

    <v-textarea
      v-model="statement.one"
      placeholder="Erste Aussage hinzufügen"
      rows="3"
      row-height="5"
    ></v-textarea>
    <v-textarea
      v-model="statement.two"
      placeholder="Zweite Aussage hinzufügen"
      rows="3"
      row-height="5"
    ></v-textarea>

    <v-radio
      v-for="item in [
        { key: 'one', value: 'Erste Aussage' },
        { key: 'two', value: 'Zweite Aussage' },
      ]"
      :key="item.key"
      :value="item.key"
      :label="item.value"
      v-model="statement.correct"
    />
  </div>
</template>

<script>
export default {
  props: {
    statement: Object,
  },
};
</script>

<style lang="scss" scoped>
.rightanswer {
  margin-top: 1rem;
  display: flex;
  flex-wrap: wrap;
  padding: 0.4rem;

  h3 {
    margin-bottom: 0.5rem;
    width: 100%;
  }

  .v-radio {
    width: 50%;
  }

  .v-radio,
  .v-textarea {
    margin-top: 1rem;
  }
}
</style>