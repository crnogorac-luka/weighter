<script>
export default {
  props: {
    currentWeight: Number,
  },
  data() {
    return {
      editMode: false,
      newWeight: 72,
    };
  },
  methods: {
    changeWeight: function (e) {
      e.preventDefault();
      this.$emit("changeweight", this.newWeight);
      this.editMode = !this.editMode;
      //console.log(this.currentWeight);
    },
  },
};
</script>

<template>
  <div id="currentWeight">
    <h2>CURRENT WEIGHT</h2>
    <div id="weightNum" v-if="!this.editMode">
      <span>{{ currentWeight }}</span>
      <span>kg</span>
    </div>
    <form v-if="this.editMode" id="weightForm" @submit="changeWeight">
      <input
        type="number"
        min="10"
        max="250"
        name="newWeight"
        v-model="newWeight"
      />
      <button type="submit">SAVE</button>
    </form>
    <button v-if="!this.editMode" @click="this.editMode = !this.editMode">
      EDIT
    </button>
  </div>
</template>

<style lang="scss" scoped>
@import "../assets/colors.scss";
@import "../assets/typography.scss";
@import "../assets/buttons.scss";
@import "../assets/shadows.scss";

#currentWeight {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  height: fit-content;
  background-color: $primaryGreen;
  padding: 2rem;
  border-radius: 16px;
  box-shadow: $softShadow;
  max-width: 400px;
  min-width: 320px;

  h2 {
    @include sectionTitle;
    margin: 0;
    color: white;
  }

  #weightNum {
    color: white;

    span:first-child {
      @include bigText;
      margin-right: 0.8rem;
    }
  }

  button {
    @include button1;
    @include buttonText;
    color: $primaryGreen;
    background-color: white;
  }

  form {
    display: flex;
    flex-direction: column;
    gap: 10px;

    input {
      width: 50%;
      height: fit-content;
      background-color: rgba(255, 255, 255, 0.171);
      border: 0;

      color: white;
      @include bigText;
    }

    input:focus {
      outline: none;
    }
  }
}
</style>
