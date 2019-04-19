# 1.1.2_Frontend Interview Tests - Calendar and DatePicker
   
>component for Vue.js  
 
## installation

``` bash
npm install
```

## Development

``` bash
npm run dev
```

## API

### Props

| Name   | Type       | Default |Description                                       |
| :----- | :-------   | :----   |:------------------------------------------------ |
| selected  | Object  |         |Set the default value for the selectd date.if not setting, the default value is current date.        |
| border    | Boolean | false   |show the date field border or not                           |
| weekTitle | Array   |         |rewirte the date field name of title                        |  
| changedate   | function(value)  |        | when a date has been selected,update the value.     |
| datepickerShowdate  | function(value)  |        |  when a date has been selected,show the value on the input field  |     

### Events

| Name   | Description |
| :----- | :---------- |
| selectDate(item)  | select a date |
| selectMonth(item) | select a month |
| selectYear(item)  | select a year |
| selectPre() | move to the previous days, months, or years'group. |
| selectNext() | move to the next days, months, or years'group. |



