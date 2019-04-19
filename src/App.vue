<template>
  <div id="app">
    <div class="demo">
      <div class="task">
        <h2>Task 1. Calendar Component</h2>
        <calendar
          @show-date="changedate"
          :parValue="selected"
          :weekList="weekTitle"
          :hasLine="border"
        ></calendar>
      </div>
      <div class="task">
        <h2>Task 2. DatePicker Component</h2>
        <datepicker></datepicker>
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld";
import calendar from "./components/calendar";
import datepicker from "./components/datepicker";

export default {
  name: "App",
  components: {
    calendar,
    datepicker
  },
  data() {
    return {
      selected: {
        showYear: 2019,
        showMonth: 2,
        showDay: 14
      }, //指定一開始被選取的日期,可以不指定
      border: false, //指定日期是否有邊框線
      weekTitle: [
        { label: "Sun" },
        { label: "Mon" },
        { label: "Tue" },
        { label: "Wed" },
        { label: "Thu" },
        { label: "Fri" },
        { label: "Sat" }
      ] //更改日期欄位上顯示星期幾的名稱
    };
  },
  methods: {
    changedate(value) {
      this.selected.showYear = value[0];
      this.selected.showMonth = value[1];
      this.selected.showDay = value[2];
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  font-family: "Noto Sans TC", "WenQuanYi Zen Hei", "Heiti TC", Helvetica,
    "Microsoft YaHei", "Microsoft JhengHei", Arial, sans-serif;
}

.demo {
  margin: 50px auto;
  font-size: 0;
}

.task {
  width: 40%;
  display: inline-block;
  vertical-align: top;
  margin: 0 5%;
}

.task h2 {
  font-size: 20px;
  line-height: 2;
  letter-spacing: 1.5px;
  color: #666;
  text-align: center;
  margin: 0 0 16px;
}

@media screen and (max-width: 768px) {
  .task {
    width: 90%;
    display: block;
    margin: 0 auto 24px;
  }

  .task h2 {
    font-size: 16px;
  }
}
</style>
