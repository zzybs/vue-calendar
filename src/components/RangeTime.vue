<template>
    <div>
        <input size="50" type="text" @click.stop="open($event)" v-model="calendar.items.text" placeholder="区间选择" />
        <Calendar :show="calendar.show" :type="calendar.items.type" :value="calendar.items.value" :x="calendar.x" :y="calendar.y" :begin="calendar.items.begin"
            @cancel="dateCancel" @ok="dateOk" :end="calendar.items.end" :sep="calendar.items.sep" :single="calendar.items.single" :rangeValue='calendar.items.rangeValue'
            :autoclose='calendar.items.autoclose'>
        </Calendar>

        <div><router-link to="/">回到菜单</router-link></div>
    </div>
</template>
<script>
    import Calendar from './Calendar.vue'


    export default {
        name: 'rangeTime',
        components: {
            Calendar
        },
        data() {
            return {
                // 数据绑定
                calendar: {
                    show: false,
                    x: 0,
                    y: 0,
                    items: {
                        type: "date",
                        // begin: "2016-08-20",
                        // end: "2016-08-25",
                        value: "2017-03-08",
                        text: '2017-03-08~2018-03-08',
                        rangeValue: "2018-03-08",
                        sep: "-",
                        single: false,
                        autoclose: false,
                        weeks: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
                        months: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
                    }
                }
            }
        },
        // 处理值的传递
        watch: {
            'calendar.value': function (value) {
                this.calendar.items[this.calendar.picker].value = value
            }
        },
        methods: {
            // 打开显示选择器
            open(e, type) {
                // 设置类型
                this.calendar.show = true
                this.calendar.x = e.target.offsetLeft
                this.calendar.y = e.target.offsetTop + e.target.offsetHeight + 8
            },
            dateCancel(obj) {
                this.calendar.show = obj.show;
            },
            dateOk(obj) {
                this.calendar.items.text = obj.values[0] + '~' + obj.values[obj.values.length - 1];
                this.calendar.items.value = obj.values[0];
                this.calendar.items.rangeValue = obj.values[obj.values.length - 1];
            }
        }
    }
</script>