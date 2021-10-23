<template>
    <div>
        <v-input
          v-model="janein.frage"
          :value="janein.frage"
          placeholder="Wahr oder falsch?"
        ></v-input>
        <div class="rightanswer">
            <h3>Welches ist die richtige Antwort?</h3>
          <v-radio
            v-for="item in [{key: 'ja', value: 'Ja'}, {key: 'nein', value: 'Nein'}]"
            :key="item.key"
            :value="item.key"
            :label="item.value"
            v-model="janein.correct"
          />
        </div>
      </div>
</template>

<script>
export default {
  props: {
    janein: Object,
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

  button {
    width: 50%;
    margin-top: 0.4rem;
  }
}
</style>