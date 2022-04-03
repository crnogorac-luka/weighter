<script>
//let goalPrc = calculateGoal();

export default {
  props: {
    goal: Number,
    currentWeight: Number,
  },
  data() {
    return {
      editMode: false,
      newGoal: 70,
    };
  },
  methods: {
    donutOffset() {
      let percentage = Math.floor((this.goal * 100) / this.currentWeight);
      return {
        value: percentage,
        style: {
          "stroke-dashoffset": "calc(440 - (440 * " + percentage + ") / 100)",
        },
      };
    },
    changeGoal: function (e) {
      e.preventDefault();
      this.$emit("changegoal", this.newGoal);
      this.editMode = !this.editMode;
      //console.log(this.currentWeight);
    },
  },
};
</script>

<template>
  <div id="goalStatus">
    <h2>REACHING THE GOAL</h2>
    <div id="goal box">
      <div class="percent">
        <svg>
          <circle cx="70" cy="70" r="70"></circle>
          <circle cx="70" cy="70" r="70" :style="donutOffset().style"></circle>
        </svg>
        <div class="num">
          <h3>
            {{ donutOffset().value }}
            <span>%</span>
          </h3>
        </div>
      </div>
    </div>
    <div>
      <form v-if="this.editMode" id="weightForm" @submit="changeGoal">
        <input
          type="number"
          min="10"
          max="250"
          name="newGoal"
          v-model="newGoal"
        />
        <button type="submit">SAVE</button>
      </form>
      <h3 v-if="!this.editMode">
        GOAL: <span>{{ goal }} kg</span>
      </h3>
      <button v-if="!this.editMode" @click="this.editMode = !this.editMode">
        CHANGE GOAL
      </button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "../assets/colors.scss";
@import "../assets/typography.scss";
@import "../assets/buttons.scss";
@import "../assets/shadows.scss";

#goalStatus {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  height: fit-content;
  width: 320px;

  h2 {
    @include sectionTitle;
    margin: 0;
    color: $primaryGreen;
  }
  button {
    @include button1;
    @include buttonText;
    color: white;
    background-color: $primaryGreen;
    width: fit-content;
    padding-left: 2rem;
    padding-right: 2rem;
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

      color: $primaryGreen;
      @include bigText;
    }

    input:focus {
      outline: none;
    }
  }

  .percent {
    position: relative;
    width: 150px;
    height: 150px;
    border-radius: 50%;
    background: rgb(255, 255, 255);
    z-index: 1000;

    svg {
      position: relative;
      width: 150px;
      height: 150px;
      z-index: 1000;

      circle {
        width: 100%;
        height: 100%;
        fill: none;
        stroke: $lightGrey;
        stroke-width: 10;
        stroke-linecap: round;
        transform: translate(5px, 5px);
      }

      circle:nth-child(2) {
        stroke-dasharray: 440;
        stroke-dashoffset: 440;
      }

      circle:nth-child(2) {
        stroke: $primaryGreen;
      }
    }

    .num {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 50%;

      h3 {
        color: #777;
        font-weight: 700;
        font-size: 40px;
        transition: 0.5s;

        span {
          color: #777;
          font-size: 24px;
          transition: 0.5s;
        }
      }
    }
  }
}
</style>
