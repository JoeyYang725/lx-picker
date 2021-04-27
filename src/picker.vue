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
  props: {
    //
    readOnly: { type: Boolean, default: false },
    value: { type: String, default: "" },
    format: { type: String, default: "YYYY-MM-DD" },
    name: { type: String, default: "" },
    inputAttr: Object,
    inputStyle: [Object, Array],
    inputClass: [Object, Array],
    calendarAttr: Object,
    calendarStyle: [Object, Array],
    calendarClass: [Object, Array],
    disabledDate: { type: Function, default: () => false },
  },
  data() {
    return {
      show: false,
      days: ["Su", "Mo", "Tu", "We", "Th", "Fr", "Sa"],
      months: [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec",
      ],
      date: [],
      now: new Date(),
      pickedValue: "",
    };
  },
  watch: {
    now() {
      this.update();
    },
    show() {
      this.update();
    },
  },
  methods: {
    close() {
      this.show = false;
    },
    update() {},
    //点击改变年份
    yearClick(flag) {
      this.now.setFullYear(this.now.getFullYear() + flag);
      this.now = new Date(this.now);
    },
    //点击改变月份
    monthClick(flag) {
      this.now.setMonth(this.now.getMonth() + flag, 1);
      this.now = new Date(this.now);
    },
    pickDate(index) {
      this.show = false;
      this.now = new Date(this.date[index].time);
      this.pickedValue = this.stringify();
    },
    parse(str) {
      let time = new Date(str);
      return isNaN(time.getTime()) ? null : time;
    },
    stringify(time = this.now, format = this.format) {
      let year = time.getFullYear();
      let month = time.getMonth() + 1;
      let date = time.getDate();
      let monthName = this.months[time.getMonth()];
      let map = {
        YYYY: year,
        MMM: monthName,
        MM: ("0" + month).slice(-2),
        M: month,
        DD: ("0" + month).slice(-2),
        D: date,
      };
      return format.replace(/Y+|M+|D+/g, function (str) {
        return map[str];
      });
    },
    leave(e) {
      if (!this.$el.contains(e.target)) {
        this.close();
      }
    },
  },
  mounted() {
    this.pickedValue = this.value;
    this.$nextTick(() => {
      this.now = this.parse(this.pickedValue) || new Date();
      document.addEventListener("click", this.leave, false);
    });
  },
  beforeDestroy() {
    document.removeEventListener("click", this.leave, false);
  },
};
</script>
<style scoped></style>
