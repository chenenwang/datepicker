<template>
  <div class="calendar-wrap">
    <div class="calendar-head">
      <div class="calendar-head-option">
        <transition name="slide-title">
          <div class="calendar-vue-day" v-show="panelType == 'day'">
            <div class="calendar-head-content" @click="panelType = 'month'">
              <span>{{tmpYear}}</span>
              <span>{{changeTmpMonth}}</span>
            </div>
          </div>
        </transition>
        <transition name="slide-title">
          <div class="calendar-vue-month" v-show="panelType == 'month'">
            <div class="calendar-head-content" @click="panelType = 'year'">
              <span>{{tmpYear}}</span>
            </div>
          </div>
        </transition>
        <transition name="slide-title">
          <div class="calendar-vue-year" v-show="panelType == 'year'">
            <div class="calendar-head-content">
              <span>{{ yearList[0]}} - {{ yearList[11]}}</span>
            </div>
          </div>
        </transition>
        <div class="calendar-btn pre" @click="selectPre()"></div>
        <div class="calendar-btn next" @click="selectNext()"></div>
      </div>
    </div>
    <div class="calendar-body">
      <transition name="slide-fade">
        <div class="calendar-vue-day_type" :class="{hasLine:hasLine}" v-show="panelType == 'day'">
          <ul class="calendar-body-title">
            <li v-for="(item, index) in weekList" :key="index" v-text="item.label"></li>
          </ul>
          <ul class="calendar-body-box">
            <li
              v-for="(item, index) in dateList"
              :key="index"
              v-text="item.value"
              :class="{pre: item.previousMonth, next: item.nextMonth, curry: date === item.value && month === tmpMonth && year === tmpYear && item.currentMonth, choose: nowValue === item.value && item.currentMonth}"
              @click="selectDate(item)"
            ></li>
          </ul>
        </div>
      </transition>
      <transition name="slide-fade">
        <div class="calendar-vue-month_type" v-show="panelType == 'month'">
          <ul class="calendar-body-box">
            <li
              v-for="(item, index) in monthList"
              :key="index"
              v-text="item.label"
              :class="{choose:item.value == tmpMonth}"
              @click="selectMonth(item)"
            ></li>
          </ul>
        </div>
      </transition>
      <transition name="slide-fade">
        <div class="calendar-vue-year_type" v-show="panelType == 'year'">
          <ul class="calendar-body-box">
            <li
              v-for="(item,index) in yearList"
              :key="index"
              v-text="item"
              :class="{choose:item === tmpYear && fixedYear === 0}"
              @click="selectYear(item)"
            ></li>
          </ul>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: new Date().getDate(), // 當前日期
      month: new Date().getMonth(), // 當前月份
      year: new Date().getFullYear(), // 當前年份
      tmpMonth: this.parValue.showMonth - 1, // 臨時月份，可修改
      tmpYear: this.parValue.showYear, // 臨時年份，可修改
      fixedYear: 0, // 年份面板鎖定
      monthList: [
        { label: "Jan", value: 0, fullname: "January" },
        { label: "Feb", value: 1, fullname: "February" },
        { label: "Mar", value: 2, fullname: "March" },
        { label: "Apr", value: 3, fullname: "April" },
        { label: "May", value: 4, fullname: "May" },
        { label: "Jun", value: 5, fullname: "June" },
        { label: "Jul", value: 6, fullname: "July" },
        { label: "Aug", value: 7, fullname: "August" },
        { label: "Sept", value: 8, fullname: "September" },
        { label: "Oct", value: 9, fullname: "October" },
        { label: "Nov", value: 10, fullname: "November" },
        { label: "Dec", value: 11, fullname: "December" }
      ], // 月
      nowValue: this.parValue.showDay, // 當前選中之日期值
      panelType: "day" // 面板狀態
    };
  },
  props: {
    parValue: {
      default: function() {
        return {
          showYear: new Date().getFullYear(),
          showMonth: new Date().getMonth() + 1,
          showDay: new Date().getDate()
        };
      }
    },
    hasLine: {
      type: Boolean,
      default() {
        return false;
      }
    },
    weekList: {
      default: function() {
        return [
          { label: "Sun" },
          { label: "Mon" },
          { label: "Tue" },
          { label: "Wed" },
          { label: "Thu" },
          { label: "Fri" },
          { label: "Sat" }
        ];
      }
    }
  },
  methods: {
    selectDate(item) {
      // 賦予當前nowValue,用於控制樣式突出顯示
      this.nowValue = item.value;
      // 如選擇到上個月
      if (item.previousMonth) {
        // 如選擇到上個年
        if (this.tmpMonth > 0) {
          this.tmpMonth -= 1;
        } else {
          this.tmpYear -= 1;
          this.tmpMonth = 11;
        }
      }
      // 如選擇到下個月
      if (item.nextMonth) {
        // 如選擇到下個年
        if (this.tmpMonth < 11) {
          this.tmpMonth += 1;
        } else {
          this.tmpYear += 1;
          this.tmpMonth = 0;
        }
      }
      // 賦予一筆陣列值並傳送到外部
      let selectDay = [this.tmpYear, this.tmpMonth + 1, this.nowValue];
      this.$emit("show-date", selectDay);
    },
    selectMonth(item) {
      this.tmpMonth = item.value;
      this.panelType = "day";
    },
    selectYear(item) {
      this.tmpYear = item;
      this.fixedYear = 0;
      this.panelType = "month";
    },
    selectPre() {
      let preMongthLength = new Date(this.tmpYear, this.tmpMonth, 0).getDate();
      if (this.panelType === "year") {
        this.tmpYear -= 12;
        this.fixedYear -= 1;
      } else if (this.panelType === "month") {
        if (this.tmpMonth > 0) {
          this.tmpMonth -= 1;
        } else {
          this.tmpYear -= 1;
          this.tmpMonth = 11;
        }
      } else if (this.panelType === "day") {
        if (this.nowValue > 1) {
          this.nowValue -= 1;
        } else {
          if (this.tmpMonth > 0) {
            this.tmpMonth -= 1;
          } else {
            this.tmpYear -= 1;
            this.tmpMonth = 11;
          }
          this.nowValue = preMongthLength;
        }
      }
    },
    selectNext() {
      let curMongthLength = new Date(
        this.tmpYear,
        this.tmpMonth + 1,
        0
      ).getDate();
      if (this.panelType === "year") {
        this.tmpYear += 12;
        this.fixedYear += 1;
      } else if (this.panelType === "month") {
        if (this.tmpMonth < 11) {
          this.tmpMonth += 1;
        } else {
          this.tmpYear += 1;
          this.tmpMonth = 0;
        }
      } else if (this.panelType === "day") {
        if (this.nowValue < curMongthLength) {
          this.nowValue += 1;
        } else {
          if (this.tmpMonth < 11) {
            this.tmpMonth += 1;
          } else {
            this.tmpYear += 1;
            this.tmpMonth = 0;
          }
          this.nowValue = 1;
        }
      }
    }
  },
  computed: {
    dateList() {
      //獲取當月的總天數
      let currentMonthLength = new Date(
        this.tmpYear,
        this.tmpMonth + 1,
        0
      ).getDate();
      //先將當月的日期塞入dateList
      let dateList = Array.from(
        { length: currentMonthLength },
        (val, index) => {
          return {
            currentMonth: true,
            value: index + 1
          };
        }
      );
      // 獲取當月1號的星期以確定需要在前插入多少天
      let startDay = new Date(this.tmpYear, this.tmpMonth, 1).getDay();
      // 確認上個月的總天數
      let previousMongthLength = new Date(
        this.tmpYear,
        this.tmpMonth,
        0
      ).getDate();
      // 在1號前插入上個月的日期
      for (let i = 0, len = startDay; i < len; i++) {
        dateList = [
          { previousMonth: true, value: previousMongthLength - i }
        ].concat(dateList);
      }
      // 補足剩餘的天數
      for (let i = 1, item = dateList.length; i < 43 - item; i++) {
        dateList[dateList.length] = { nextMonth: true, value: i };
      }
      return dateList;
    },
    changeTmpMonth() {
      return this.monthList[this.tmpMonth].fullname;
    },
    yearList() {
      let curryYear = Math.floor(this.tmpYear / 12);
      let curryYearList = Array.from(
        { length: 12 },
        (value, index) => curryYear * 12 + index
      );
      return curryYearList;
    }
  }
};
</script>

<style>
.calendar-wrap {
  width: 100%;
  min-width: 300px;
  max-width: 480px;
  margin: auto;
  background: #fff;
  text-align: center;
  -webkit-box-shadow: 2px 2px 24px 0 rgba(0, 0, 0, 0.2);
  box-shadow: 2px 2px 24px 0 rgba(0, 0, 0, 0.2);
  border-radius: 12px;
  overflow: hidden;
  font-size: 0;
}

.calendar-head {
  position: relative;
  background: #db3d44;
}

.calendar-head-option {
  height: 50px;
  padding: 0 60px;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

.calendar-head-content {
  display: inline-block;
  cursor: pointer;
}

.calendar-head-content:hover {
  text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.5);
}

.calendar-head-content span {
  display: inline-block;
  vertical-align: middle;
  font-size: 18px;
  font-weight: bold;
  line-height: 50px;
  letter-spacing: 2px;
  color: #fff;
  margin: 0 8px;
  -webkit-transition: 0.3s;
  transition: 0.3s;
}

.calendar-btn {
  width: 24px;
  height: 24px;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto;
  cursor: pointer;
}

.calendar-btn:hover::before {
  opacity: 1;
}

.calendar-btn::before {
  content: "";
  width: 100%;
  height: 100%;
  background: #fff;
  border-radius: 50%;
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0.6;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.calendar-btn::after {
  content: "";
  width: 6px;
  height: 6px;
  border-width: 2px 2px 0 0;
  border-style: solid;
  border-color: #db3d44;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
}

.calendar-btn.pre {
  left: 16px;
}

.calendar-btn.pre::after {
  -webkit-transform: translateX(2px) rotate(-135deg);
  transform: translateX(2px) rotate(-135deg);
}

.calendar-btn.next {
  right: 16px;
}

.calendar-btn.next::after {
  -webkit-transform: translateX(-2px) rotate(45deg);
  transform: translateX(-2px) rotate(45deg);
}

.calendar-body {
  padding: 8px;
  height: 310px;
  overflow: hidden;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

.calendar-vue-day_type.hasLine .calendar-body-box li {
  border: 1px solid #eee;
  box-sizing: border-box;
}

.calendar-body ul {
  width: 100%;
  padding: 0;
  margin: 0;
}

.calendar-body li {
  display: inline-block;
  vertical-align: middle;
  position: relative;
  font-size: 15px;
  color: #333;
}

.calendar-body li.next,
.calendar-body li.pre {
  color: #eee;
}

.calendar-body li.curry {
  color: #db3d44;
}

.calendar-body li.choose {
  color: #fff;
}

.calendar-body li.choose::before {
  -webkit-transform: scale(1);
  transform: scale(1);
  background: #db3d44;
}

.calendar-body-box li {
  cursor: pointer;
  z-index: 1;
}

.calendar-body-box li::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
  border-radius: 50%;
  z-index: -1;
  -webkit-transform: scale(0);
  transform: scale(0);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  -webkit-box-shadow: 0 0 0 1px #db3d44;
  box-shadow: 0 0 0 1px #db3d44;
}

.calendar-body-box li:hover::before {
  -webkit-transform: scale(1);
  transform: scale(1);
}

.calendar-vue-day_type li {
  width: 14.28%;
  height: 42px;
  line-height: 42px;
}

.calendar-vue-day_type .calendar-body-box li::before {
  width: 36px;
  height: 36px;
}

.calendar-vue-month_type li,
.calendar-vue-year_type li {
  width: 33.3%;
  height: 73.5px;
  line-height: 73.5px;
}

.calendar-vue-month_type .calendar-body-box li::before,
.calendar-vue-year_type .calendar-body-box li::before {
  width: 56px;
  height: 56px;
}

.fadeInDownBig,
.fadeDownBig-enter-active,
.fadeDownBig-leave-active {
  -webkit-animation: 0.2s linear both;
  animation: 0.2s linear both;
}

.fadeDownBig-enter-active {
  -webkit-animation-name: fadeInDownBig;
  animation-name: fadeInDownBig;
}

.fadeDownBig-leave-active {
  -webkit-animation-name: fadeOutDownBig;
  animation-name: fadeOutDownBig;
}

@-webkit-keyframes fadeInDownBig {
  0% {
    opacity: 0;
    -webkit-transform: translateY(-8px);
    transform: translateY(-8px);
  }
  100% {
    opacity: 1;
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
}

@keyframes fadeInDownBig {
  0% {
    opacity: 0;
    -webkit-transform: translateY(-8px);
    transform: translateY(-8px);
  }
  100% {
    opacity: 1;
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
}

@-webkit-keyframes fadeOutDownBig {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    -webkit-transform: translateY(-8px);
    transform: translateY(-8px);
  }
}

@keyframes fadeOutDownBig {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    -webkit-transform: translateY(-8px);
    transform: translateY(-8px);
  }
}

.slide-title-enter-active,
.slide-title-leave-active {
  -webkit-transition: 0.3s ease;
  transition: 0.3s ease;
}

.slide-title-enter,
.slide-title-leave-to {
  -webkit-transform: translateY(12px);
  transform: translateY(12px);
  opacity: 0;
}

.slide-fade-enter-active,
.slide-fade-leave-active {
  -webkit-transition: 0.4s ease;
  transition: 0.4s ease;
}

.slide-fade-enter,
.slide-fade-leave-to {
  -webkit-transform: translateY(42%);
  transform: translateY(42%);
  opacity: 0;
}

.st0 {
  fill: none;
  stroke: #666;
  stroke-width: 3;
  stroke-miterlimit: 10;
  -webkit-transition: 0.2s;
  transition: 0.2s;
}

.st1 {
  fill-rule: evenodd;
  clip-rule: evenodd;
  fill: #ffffff;
  stroke: #666;
  stroke-width: 3;
  stroke-miterlimit: 10;
  -webkit-transition: 0.2s;
  transition: 0.2s;
}

.st2 {
  fill-rule: evenodd;
  clip-rule: evenodd;
  fill: none;
  stroke: #666;
  stroke-width: 3;
  stroke-miterlimit: 10;
  -webkit-transition: 0.2s;
  transition: 0.2s;
}
/*# sourceMappingURL=module.css.map */
</style>
