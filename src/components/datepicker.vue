<template>
  <div class="datepicker">
    <div class="input-box">
      <input
        type="text"
        v-model="dateValue"
        @click="switchCalendar =!switchCalendar"
        placeholder="Pls type or select a date"
        :class="{focus:switchCalendar}"
      >
      <svg x="0px" y="0px" viewBox="0 0 100 100" style="enable-background:new 0 0 100 100;">
        <path
          class="st0"
          d="M91.75,91H8.09C5.83,91,4,89.17,4,86.91V21.84c0-2.26,1.83-4.09,4.09-4.09h83.65c2.26,0,4.09,1.83,4.09,4.09
	v65.07C95.84,89.17,94.01,91,91.75,91z"
        ></path>
        <line class="st0" x1="5.09" y1="33.05" x2="94.75" y2="33.05"></line>
        <path
          class="st1"
          d="M22.34,24.31h-2.79c-1.34,0-2.43-1.09-2.43-2.43V11.43c0-1.34,1.09-2.43,2.43-2.43h2.79
	c1.34,0,2.43,1.09,2.43,2.43v10.44C24.77,23.22,23.68,24.31,22.34,24.31z"
        ></path>
        <path
          class="st1"
          d="M79.2,24.31H76.4c-1.34,0-2.43-1.09-2.43-2.43V11.43c0-1.34,1.09-2.43,2.43-2.43h2.79
	c1.34,0,2.43,1.09,2.43,2.43v10.44C81.63,23.22,80.54,24.31,79.2,24.31z"
        ></path>
        <path
          class="st2"
          d="M21.26,50.55h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C22.79,49.86,22.11,50.55,21.26,50.55z"
        ></path>
        <path
          class="st2"
          d="M21.26,66.95h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C22.79,66.26,22.11,66.95,21.26,66.95z"
        ></path>
        <path
          class="st2"
          d="M21.26,83.35h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C22.79,82.66,22.11,83.35,21.26,83.35z"
        ></path>
        <path
          class="st2"
          d="M37.66,50.55h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C39.19,49.86,38.51,50.55,37.66,50.55z"
        ></path>
        <path
          class="st2"
          d="M37.66,66.95h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C39.19,66.26,38.51,66.95,37.66,66.95z"
        ></path>
        <path
          class="st2"
          d="M37.66,83.35h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C39.19,82.66,38.51,83.35,37.66,83.35z"
        ></path>
        <path
          class="st2"
          d="M54.06,50.55h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C55.59,49.86,54.91,50.55,54.06,50.55z"
        ></path>
        <path
          class="st2"
          d="M54.06,66.95h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C55.59,66.26,54.91,66.95,54.06,66.95z"
        ></path>
        <path
          class="st2"
          d="M70.46,50.55h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C71.99,49.86,71.31,50.55,70.46,50.55z"
        ></path>
        <path
          class="st2"
          d="M70.46,66.95h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C71.99,66.26,71.31,66.95,70.46,66.95z"
        ></path>
        <path
          class="st2"
          d="M86.86,50.55h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C88.39,49.86,87.71,50.55,86.86,50.55z"
        ></path>
        <path
          class="st2"
          d="M86.86,66.95h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C88.39,66.26,87.71,66.95,86.86,66.95z"
        ></path>
        <path
          class="st2"
          d="M54.06,83.35h-7.88c-0.84,0-1.53-0.68-1.53-1.53v-7.88c0-0.84,0.68-1.53,1.53-1.53h7.88
	c0.84,0,1.53,0.68,1.53,1.53v7.88C55.59,82.66,54.91,83.35,54.06,83.35z"
        ></path>
      </svg>
    </div>
    <transition name="fadeDownBig">
      <calendar v-show="switchCalendar" @show-date="datepickerShowdate"></calendar>
    </transition>
  </div>
</template>



<script>
import calendar from "./calendar";

export default {
  components: {
    calendar
  },
  data() {
    return {
      dateValue: "",
      switchCalendar: false
    };
  },
  methods: {
    datepickerShowdate(value) {
      this.switchCalendar = false;
      if (value[1] < 10) {
        value[1] = "0" + value[1];
      }
      if (value[2] < 10) {
        value[2] = "0" + value[2];
      }
      this.dateValue = value[0] + "-" + value[1] + "-" + value[2];
    }
  }
};
</script>

<style>
.datepicker {
  width: 100%;
  min-width: 300px;
  max-width: 480px;
  margin: auto;
  position: relative;
}

.datepicker .calendar-wrap {
  position: absolute;
  left: 0;
  top: 120%;
}

.datepicker .input-box {
  width: 100%;
  position: relative;
}

.datepicker .input-box svg {
  width: 32px;
  height: 32px;
  position: absolute;
  left: 12px;
  top: 0;
  bottom: 0;
  margin: auto;
}

.datepicker .input-box input {
  -moz-appearance: none;
  -webkit-appearance: none;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  outline: 0;
  margin: 0;
  padding: 0 12px 0 56px;
  width: 100%;
  height: 48px;
  font-size: 16px;
  line-height: 48px;
  letter-spacing: 1px;
  color: #333;
  border: 1.5px solid #ddd;
  border-radius: 8px;
  -webkit-transition: 0.3s;
  transition: 0.3s;
}

.datepicker .input-box input.focus {
  color: #db3d44;
  border: 1.5px solid #db3d44;
}

.datepicker .input-box input.focus + svg .st0,
.datepicker .input-box input.focus + svg .st1,
.datepicker .input-box input.focus + svg .st2 {
  stroke: #db3d44;
}
</style>
