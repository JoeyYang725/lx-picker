<template>
  <div class="lx-picker">
    <input type="text" />
    <div class="picker-wrap">
      <table class="date-picker">
        <thead>
          <tr class="date-head">
            <th colspan="4">
              <span class="btn-prev"></span>
              <span class="show-year"></span>
              <span class="btn-next"></span>
            </th>
            <th colspan="3">
              <span class="btn-prev"></span>
              <span class="show-month"></span>
              <span class="btn-next"></span>
            </th>
          </tr>
          <tr class="date-days">
            <th v-for="day in days" :key="day">{{ day }}</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: {},
  data() {
    return {
      days: [],
    };
  },
  watch: {},
  methods: {},
  mounted() {},
  beforeDestroy() {},
};
</script>
<style scoped></style>
