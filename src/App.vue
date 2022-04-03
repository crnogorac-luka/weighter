<script setup>
import CurrentWeight from "./components/CurrentWeight.vue";
import RecentWeight from "./components/RecentWeight.vue";
import GoalStatus from "./components/GoalStatus.vue";
</script>

<script>
const today = new Date();
const todayString = today.toLocaleString("en-US", {
  year: "numeric",
  month: "numeric",
  day: "numeric",
});

function getDayBefore() {
  today.setDate(today.getDate() - 1);
  return today.toLocaleString("en-US", {
    year: "numeric",
    month: "numeric",
    day: "numeric",
  });
}

export default {
  data() {
    return {
      goal: 65,
      records: [
        {
          id: 0,
          date: todayString,
          weight: 72,
        },
        {
          id: 1,
          date: getDayBefore(),
          weight: 70,
        },
        {
          id: 2,
          date: getDayBefore(),
          weight: 69,
        },
        {
          id: 3,
          date: getDayBefore(),
          weight: 71,
        },
        {
          id: 4,
          date: getDayBefore(),
          weight: 90,
        },
        {
          id: 5,
          date: getDayBefore(),
          weight: 90,
        },
      ],
    };
  },
};
</script>

<template>
  <header>WEIGHTER</header>

  <main>
    <div>
      <CurrentWeight
        :currentWeight="records[0].weight"
        @changeweight="records[0].weight = $event"
      ></CurrentWeight>
      <GoalStatus
        :goal="goal"
        :currentWeight="records[0].weight"
        @changegoal="goal = $event"
      ></GoalStatus>
    </div>

    <RecentWeight :weightRecords="records"></RecentWeight>
  </main>
</template>

<style lang="scss">
//@import "~@/assets/scss/vendors/bootstrap-vue/index";
//@import "./assets/base.css";

@import "./assets/colors.scss";
@import "./assets/typography.scss";
@import url("https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,300;0,400;0,700;0,900;1,300;1,400;1,700;1,900&display=swap");

body {
  padding: 0 !important;
  margin: 0 !important;
  font-family: "Lato", sans-serif !important;
}

#app {
  margin: 3rem 15rem;
  display: flex;
  flex-direction: column;
  gap: 4rem;
}

header {
  width: 100%;
  height: 3rem;
  color: $primaryGreen;
  @include mainTitle;
}
main {
  display: flex;
  flex-direction: column;

  & > div {
    display: flex;
    justify-content: space-between;
    margin-bottom: 3rem;
  }
}
</style>
