<script>
export default {
  props: {
    weightRecords: Array,
  },
};
</script>

<template>
  <div id="recentWeight">
    <h2>RECENT WEIGHT</h2>
    <table>
      <thead>
        <tr>
          <th>Date</th>
          <th>Weight</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="record in this.weightRecords" :key="record.id">
          <td>{{ record.date }}</td>
          <td>{{ record.weight }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style lang="scss" scoped>
@import "../assets/colors.scss";
@import "../assets/typography.scss";
@import "../assets/buttons.scss";
@import "../assets/shadows.scss";

#recentWeight {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  height: fit-content;
  width: 40%;
  margin: 0 auto;

  h2 {
    @include sectionTitle;
    margin: 0;
    color: $primaryGreen;
  }

  table {
    thead {
      tr {
        th {
          line-height: 170%;
          text-align: left;
          border-bottom: 1px solid $lightGrey;
        }
      }
    }
  }
  tbody {
    tr:first-child {
      td {
        padding-top: 0.5rem;
      }
    }
  }
}
</style>
