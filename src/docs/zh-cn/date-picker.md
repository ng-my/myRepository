<script>
export default {
    data:()=> ({
        date1: '2015-12-06',
        date2: '2015-12-06',
        date3: '2015-12-06',
        date4: '2015-12-06',
        rangeDate1: ['2015-12-06','2016-12-06'],
        rangeDate2: ['2015-12-06','2016-12-06'],
        rangeDate3: ['2015-12-06','2016-12-06'],
        time1: '2011-11-11 11:11',
        time2: '2222-11-11 12:12',
        rangeTime1: ['2020-04-04 04:04','2022-08-08 08:08'],
        rangeTime2: ['2015-11-11 23:12','2016-12-12 23:12']
    }),
    watch: {
        date1(val){
            console.log('watch:', val)
        },
        rangeDate1(val){
            console.log('watch:', val)
        }
    },
    methods: {
        confirm() {
            console.log('confirm')
        },
        change(time) {
            console.log('change:', time)
        },
        rangeChange(startTime, endTime) {
            console.log('change:', startTime, endTime)
        },
        range (start, end){
            const result = [];
            for (let i = start; i < end; i++) {
                result.push(i);
            }
            return result;
        },
        disabledDate(current){
            return current && current.valueOf() < Date.now();
        },
        disabledTime(){
            return [{
                disabledHours: (h) => this.range(0, 24).splice(4, 20).includes(h),
                disabledMinutes: (m) => this.range(30, 60).includes(m)
            }]
        },
        disabledRangeTime(){
            return [{
                disabledHours: (h) => this.range(0, 24).splice(4, 20).includes(h),
                disabledMinutes: (m) => this.range(30, 60).includes(m)
            },{
                disabledHours: (h) => this.range(0, 60).splice(20, 4).includes(h),
                disabledMinutes: (m) => this.range(0, 31).includes(m)
            }]
        }
    }
}
</script>

# DatePicker 日期选择框

输入或选择日期的控件。

## 何时使用
当用户需要输入一个日期，可以点击标准输入框，弹出日期面板进行选择。

## 代码演示

::: demo
<summary>
  #### 基础
  最简单的用法，在浮层中可以选择或者输入日期
</summary>

```html
<template>
    <v-date-picker clearable show-time v-model="time1" @change="change"></v-date-picker>
        <v-date-picker range show-time v-model="rangeTime1" clearable></v-date-picker>
</template>
<script>
export default {
    data:()=> ({
        time1: '2015-12-06 23:12',
        rangeTime1: ['2015-12-06 23:12','2016-12-06 23:12']
    }),
    methods: {
        change(time) {
            console.log('change:', time)
        }
    }
}
</script>
```
::: demo
<summary>
  #### 日期时间选择
  增加选择时间功能
</summary>



## API
### DatePicker Props
| 参数        | 说明           | 类型               | 默认值       |
|------------|----------------|-------------------|-------------|
| value  | 默认日期,当range为true时为数组[开始时间，结束时间] | string/array | - |
| size | 输入框大小，lg 高度为 32px，sm 为 22px，默认是 28px | string | - |
| placeholder  | 占位提示符 | string | 请选择日期 |
| position | 下拉框的定位方式(absolute、fixed) | string | absolute |
| popupContainer | 下拉菜单渲染父节点。默认渲染到 body 上，如果你遇到菜单滚动定位问题，试试修改为滚动的区域，并相对其定位。 | function | () => document.body |
| range | 能否进行范围选择 | boolean | false |
| showTime  | 增加时间选择功能	 | boolean | false |
| maxRange | 选择最大范围限制,以天为单位（只有range为true的时候才起作用） | number | - |
| clearable | 是否显示清除按钮 | boolean | false |
| format  | 展示的日期格式 | string | yyyy-MM-dd |
| disabled | 禁用 | boolean | false |

### DatePicker Events
| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| change | 时间发生变化的时候触发 | time or (startTime, endTime) |
| confirm | 点击确定按钮时触发	 | - |
