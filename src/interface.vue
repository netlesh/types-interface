<template>
  <div id="modules">
    <v-select
      v-if="module"
      v-model="module.type"
      :items="items"
      label="Module Type"
      placeholder="Bitte Modul auswählen"
      item-text="key"
      item-value="value"
    >
      <template #prepend v-if="icon">
        <v-icon :name="icon" />
      </template>
    </v-select>
    <div class="module-elements">
      <modtext
        v-model:modtext="module.modtext"
        v-if="module.type === 'modtext'"
      />

      <!-- Corresponding code here. Probably needs more props and to be working with the rest -->
      <imgtext
        v-model:imgtext="module.imgtext"
        v-if="module.type === 'imgtext'"
      />
      <justimg
        v-model:justimg="module.justimg"
        v-if="module.type === 'justimg'"
      />

      <janein :janein="module.janein" v-if="module.type === 'janein'" />
      <multiple :multiple="module.multiple" v-if="module.type === 'multiple'" />
      <answers :answers="module.answers" v-if="module.type === 'answers'" />
      <statement
        :statement="module.statement"
        v-if="module.type === 'statement'"
      />
    </div>
  </div>
</template>

<script>
import janein from "./types/janein/janein.vue";
import multiple from "./types/multiple/multiple.vue";
import answers from "./types/answers/answers.vue";
import statement from "./types/statement/statement.vue";
import modtext from "./types/modtext/index.vue";
import imgtext from "./types/imgtext/index.vue";
import justimg from "./types/justimg/index.vue";

export default {
  emits: ["input"],
  components: {
    janein,
    multiple,
    answers,
    statement,
    modtext,
    imgtext,
    justimg,
  },
  props: {
    collection: {
      type: String,
      default: null,
    },
    value: {
      type: Object,
      default() {
        return {
          type: "",
          modtext: "",
          imgtext: {
            img: "",
            txt: "",
          },
          justimg: {
            id: "",
            type: "",
            filename_download: "",
          },
          janein: {
            frage: "",
            correct: "",
          },
          multiple: {
            frage: "",
            optionen: [],
            correct: "",
          },
          answers: {
            frage: "",
            optionen: [],
            correct: "",
          },
          statement: {
            one: "",
            two: "",
            correct: "",
          },
        };
      },
    },
    field: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      items: [
        { key: "Text", value: "modtext" },
        { key: "ImageText", value: "imgtext" },
        { key: "JustImage", value: "justimg" },
        { key: "Ja/Nein", value: "janein" },
        { key: "Multiple Choice", value: "multiple" },
        { key: "Multiple Answers", value: "answers" },
        { key: "Korrekte Aussage", value: "statement" },
      ],
      module: {
        type: "",
        modtext: "",
        imgtext: {
          img: "",
          txt: "",
        },
        justimg: {
          id: "",
          type: "",
          filename_download: "",
        },
        janein: {
          frage: "",
          correct: "",
        },
        multiple: {
          frage: "",
          optionen: [],
          correct: "",
        },
        answers: {
          frage: "",
          optionen: [],
          correct: [],
        },
        statement: {
          one: "",
          two: "",
          correct: "",
        },
      },
    };
  },
  watch: {
    module: {
      deep: true,
      handler(newValue) {
        console.log("watch module", newValue);
        this.emitValues(newValue);
      },
    },
    value: {
      deep: true,
      handler(newValue) {
        // Only fire when this.module is updated
        if (!newValue.type) return;
        console.log("watch value", newValue);
        if (JSON.stringify(newValue) !== JSON.stringify(this.module))
          this.module = JSON.parse(JSON.stringify(newValue));
      },
    },
  },
  methods: {
    emitValues(newValue) {
      console.log("emit change");
      this.$emit("input", newValue);
    },
  },
};
</script>

<style lang="scss">
#modules {
  .module-elements {
    border: var(--border-width) solid var(--border-normal);
    border-radius: var(--border-radius);
    margin-top: 1rem;
    padding: 1rem;
  }
}
</style>