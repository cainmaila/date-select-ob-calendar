<template>
    <div class="ob">
        <div class="head">
            <div class="bn back" @click="back">V</div>
            <div>{{dateListData.yy}}年 {{dateListData.mm+1}}月</div>
            <div class="bn next" @click="next">V</div>
        </div>
        <div>
            <div class="dd we sd">日</div>
            <div class="dd we">一</div>
            <div class="dd we">二</div>
            <div class="dd we">三</div>
            <div class="dd we">四</div>
            <div class="dd we">五</div>
            <div class="dd we sd2">六</div>
        </div>
        <div>
            <div class="dd" :class="{sd:key%7===0,sd2:key%7===6}" v-for="(date,key) in dateList" :key="key">
                <div :class="{se:date.mm === nowMon,oth:date.mm !== nowMon,today:dateOb.isToday(date)}" @click="select(date)">{{date.dd}}</div>
            </div>
            <div class="clear"> </div>
        </div>
        <div class="rest" @click="rest">重置</div>
    </div>
</template>
<script>
import DeteSelectOb from 'date-select-ob'
export default {
    data() {
        return {
            dateOb: null,
            dateListData: {}
        }
    },
    computed: {
        dateList() {
            return this.dateListData.list
        },
        nowMon() {
            return this.dateListData.mm
        }
    },
    components: {},
    methods: {
        rest() {
            this.dateListData = this.dateOb.rest()
            this.$emit('rest')
        },
        next() {
            this.dateListData = this.dateOb.next()
        },
        back() {
            this.dateListData = this.dateOb.back()
        },
        select(date) {
            if (
                date.mm === this.dateListData.mm &&
                date.yy === this.dateListData.yy
            ) {
                this.$emit('select', date)
            }
        }
    },
    created() {
        this.dateOb = new DeteSelectOb()
        this.dateListData = this.dateOb.getDate()
    }
}
</script>
<style lang="less" scoped>
@ddsize: 40px;
.ob {
    position: absolute;
    top: 0px;
    left: 0px;
    width: calc(~'@{ddsize} * 9 + 2px + 10px');
    border-top: 1px solid #e3e3e3;
    border-left: 1px solid #e3e3e3;
    border-right: 1px solid #e3e3e3;
    box-sizing: border-box;
    box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.5);
    border-radius: 3px;
    z-index: 1000;
    background-color: #ffffff;
    text-align: center;
    .head {
        position: relative;
        padding-top: 20px;
        font-size: 16px;
        line-height: 40px;
        font-weight: bold;
        .bn {
            position: absolute;
            font-weight: normal;
            top: 20px;
            font-size: 12px;
            color: #b3b3b3;
            cursor: pointer;
            &:hover {
                color: #000000;
            }
            &.next {
                right: 20px;
                transform: scale(1, 1.5) rotate(-90deg);
            }
            &.back {
                left: 20px;
                transform: scale(1, 1.5) rotate(90deg);
            }
        }
    }
    .dd {
        text-align: center;
        float: left;
        width: @ddsize;
        height: @ddsize;
        padding: 5px;
        border-bottom: 1px solid #e3e3e3;
        line-height: calc(~'@{ddsize} - 10px');
        &.sd {
            padding-left: 10px;
            width: calc(~'@{ddsize} + 5px');
        }
        &.sd2 {
            padding-right: 10px;
            width: calc(~'@{ddsize} + 5px');
        }
        &.we {
            font-size: 10px;
            border-bottom: none;
        }
        .se {
            width: calc(~'@{ddsize} - 10px');
            height: calc(~'@{ddsize} - 10px');
            cursor: pointer;
            &.today {
                border-radius: 100px;
                background-color: #b3b3b3;
            }
            &:hover {
                color: #e3e3e3;
                border-radius: 100px;
                background-color: #84b926;
            }
        }
        .oth {
            width: calc(~'@{ddsize} - 10px');
            height: calc(~'@{ddsize} - 10px');
            color: #b3b3b3;
        }
    }
    .rest {
        line-height: 40px;
        border-bottom: 1px solid #e3e3e3;
        cursor: pointer;
        &:hover {
            background-color: #e3e3e3;
        }
    }
    .clear {
        clear: both;
    }
}
</style>
