<template>
  <div id="multiple">
    <v-input
      v-model="multiple.frage"
      :value="multiple.frage"
      placeholder="Nur eine Antwort stimmt auf diese Frage"
    ></v-input>
    <div class="rightanswer">
      <h3>Antwortoptionen (bitte richtige markieren):</h3>
      <v-radio
        v-for="(item, index) in multiple.optionen"
        :key="item"
        :value="item"
        :label="item"
        v-model="multiple.correct"
      >
        <template v-slot:label>
          <div class="radiolabel">
            <div class="label-text">{{ item }}</div>
            <div @click.stop="deleteAnswer(index)">
              <v-icon name="delete" />
            </div>
          </div>
        </template>
      </v-radio>
      <form
        class="custom"
        v-on:submit.prevent="addAnswer()"
        :class="{
          active: !disabled && usesOtherValue,
          'has-value': !disabled && otherValue,
          disabled,
        }"
      >
        <input v-model="neueOption" placeholder="Neue Antwort hinzufügen" />
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    multiple: Object,
  },
  data() {
    return {
      neueOption: "",
    };
  },
  methods: {
    addAnswer() {
      this.multiple.optionen.push(this.neueOption);
      this.neueOption = "";
    },
    deleteAnswer(index) {
            console.log(this.multiple)

      this.multiple.optionen.splice(index, 1);
    },
  },
};
</script>

<style lang="scss">
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
    width: 100%;
    margin-top: 1rem;
    span {
      white-space: normal !important;
      width: 100%;
    }
  }

  .radiolabel {
    display: flex;
    width: 100%;
    justify-content: space-between;
    align-items: center;
    .label-text {
      margin-right: 1rem;
    }
  }

  .custom {
    --v-icon-color: var(--foreground-subdued);
    display: flex;
    align-items: center;
    width: 100%;
    height: var(--input-height);
    padding: 10px;
    border: 2px dashed var(--border-normal);
    border-radius: var(--border-radius);
    margin-top: 1rem;

    input {
      display: block;
      flex-grow: 1;
      width: 20px; // this will auto grow with flex above
      margin: 0;
      margin-left: 8px;
      padding: 0;
      background-color: transparent;
      border: none;
      border-radius: 0;
    }
    &.has-value {
      background-color: var(--background-subdued);
      border: 2px solid var(--background-subdued);
    }
    &.active {
      --v-icon-color: var(--v-radio-color);
      position: relative;
      background-color: transparent;
      border-color: var(--v-radio-color);
      &::before {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: var(--v-radio-color);
        opacity: 0.1;
        content: "";
        pointer-events: none;
      }
    }
    &.disabled {
      background-color: var(--background-subdued);
      border-color: transparent;
      cursor: not-allowed;
      input {
        color: var(--foreground-subdued);
        cursor: not-allowed;
        &::placeholder {
          color: var(--foreground-subdued);
        }
      }
    }
  }
}
</style>