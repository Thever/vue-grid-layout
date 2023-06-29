<template>
    <!-- :layout.sync="layout" 布局顺序
    :col-num="12" 列数
    :row-height="30" 每行的高度，单位像素
    is-draggable="draggable" 是否可拖拽
    :is-resizable="resizable" 是否可调整大小
    :vertical-compact="true" 标识布局是否垂直压缩
    :use-css-transforms="true" 标识是否使用CSS属性 -->
    <grid-layout :layout.sync="layout" :col-num="12" :row-height="30" :is-draggable="draggable" :is-resizable="resizable" :vertical-compact="true" :use-css-transforms="true">
        <!-- static 是否静态（无法拖拽、调整大小或被其他元素移动）
        x 标识栅格元素位于第几列，需为自然数
        y 标识栅格元素位于第几行，需为自然数
        w 标识栅格元素的初始宽度，值为colWidth的倍数
        h 标识栅格元素的初始高度，值为rowHeight的倍数 
        w,h结合所在x,y，不能超出限制的范围，否则位置渲染会有异常
        -->
        <grid-item v-for="(item, index) in layout" :static="item.static" :x="item.x" :y="item.y" :w="item.w" :h="item.h" :i="item.i" :key="index">
            <span class="text">{{ itemTitle(item) }}</span>
        </grid-item>
    </grid-layout>
</template>

<script>
import { GridLayout, GridItem } from "vue-grid-layout"

export default {
    components: {
        GridLayout,
        GridItem
    },
    data() {
        return {
            //  布局数据
            layout: [
                { "x": 0, "y": 0, "w": 2, "h": 2, "i": "0", static: false },
                { "x": 2, "y": 0, "w": 2, "h": 4, "i": "1", static: true },
                { "x": 4, "y": 0, "w": 2, "h": 5, "i": "2", static: false },
                { "x": 6, "y": 0, "w": 2, "h": 3, "i": "3", static: false },
                { "x": 8, "y": 0, "w": 2, "h": 3, "i": "4", static: false },
                { "x": 10, "y": 0, "w": 2, "h": 3, "i": "5", static: false },
                { "x": 0, "y": 5, "w": 2, "h": 5, "i": "6", static: false },
                { "x": 2, "y": 5, "w": 2, "h": 5, "i": "7", static: false },
                { "x": 4, "y": 5, "w": 2, "h": 5, "i": "8", static: false },
                { "x": 6, "y": 3, "w": 2, "h": 4, "i": "9", static: true },
                { "x": 8, "y": 4, "w": 2, "h": 4, "i": "10", static: false },
                { "x": 10, "y": 4, "w": 2, "h": 4, "i": "11", static: false },
                { "x": 0, "y": 10, "w": 2, "h": 5, "i": "12", static: false },
                { "x": 2, "y": 10, "w": 2, "h": 5, "i": "13", static: false },
                { "x": 4, "y": 8, "w": 2, "h": 4, "i": "14", static: false },
                { "x": 6, "y": 8, "w": 2, "h": 4, "i": "15", static: false },
                { "x": 8, "y": 10, "w": 2, "h": 5, "i": "16", static: false },
                { "x": 10, "y": 4, "w": 2, "h": 2, "i": "17", static: false },
                { "x": 0, "y": 9, "w": 2, "h": 3, "i": "18", static: false },
                { "x": 2, "y": 6, "w": 2, "h": 2, "i": "19", static: false }
            ],
            //  是否可拖拽
            draggable: true,
            //  是否可调整大小
            resizable: true,
            //  无用属性
            index: 0
        }
    },
    methods: {
        itemTitle(item) {
            let result = item.i;
            if (item.static) {
                result += " - Static";
            }
            return result;
        }
    }
}
</script>

<style scoped>
.vue-grid-layout {
    background: #eee;
}

.vue-grid-item:not(.vue-grid-placeholder) {
    background: #ccc;
    border: 1px solid black;
}

.vue-grid-item .resizing {
    opacity: 0.9;
}

.vue-grid-item .static {
    background: #cce;
}

.vue-grid-item .text {
    font-size: 24px;
    text-align: center;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    height: 100%;
    width: 100%;
}

.vue-grid-item .no-drag {
    height: 100%;
    width: 100%;
}

.vue-grid-item .minMax {
    font-size: 12px;
}

.vue-grid-item .add {
    cursor: pointer;
}

.vue-draggable-handle {
    position: absolute;
    width: 20px;
    height: 20px;
    top: 0;
    left: 0;
    background: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='10' height='10'><circle cx='5' cy='5' r='5' fill='#999999'/></svg>") no-repeat;
    background-position: bottom right;
    padding: 0 8px 8px 0;
    background-repeat: no-repeat;
    background-origin: content-box;
    box-sizing: border-box;
    cursor: pointer;
}
</style>