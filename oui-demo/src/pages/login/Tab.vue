<template>
    <div class="oil-tab">
        <div
            v-for="(item, index) in tabList"
            :class="['oil-tab-item', controlIndex === index ? 'selected' : '']"
            :key="item.value"
            @click="$emit('update:controlIndex', index)"
        >
            {{item.title}}
        </div>
        <div class="oil-tab-bottomline" :style="{left: `${controlIndex * (100 / (tabs.length - 1))}%`, backgroundColor: color}"></div>
    </div>
</template>

<script>

import {mapState} from 'vuex'

export default {
    name: 'Tab',
    props: {
        controlIndex: {
            type: Number,
            default: 0
        },
        tabs: Array
    },
    computed: {
        tabList() {
            return this.tabs.filter(({hidden}) => !hidden);
        },
        ...mapState({
            color: state => state.setting.theme.color
        })
    }
}
</script>

<style lang="less">
    .oil-tab{
        width: 316px;
        display: flex;
        position: relative;
        margin-bottom: 20px;
        border-bottom: 1px solid #ccc;
        &-item{
            flex: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'SourceHanSansCN-Normal', 'Source Han Sans CN Normal', 'Source Han Sans CN', sans-serif;
            font-weight: 400;
            font-style: normal;
            font-size: 14px;
            padding: 20px 0;
            color: @text-color;
            user-select: none;
            cursor: pointer;
            &.selected{
                color: @primary-color;
            }
        }
        &-bottomline{
            width: 50%;
            height: 2px;
            position: absolute;
            bottom: -1px;
            left: 0;
            transition: left .1s linear;
        }
    }
</style>