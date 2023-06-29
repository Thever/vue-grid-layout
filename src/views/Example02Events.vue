<template>
    <div>
        <!-- 事件滚动列表 -->
        <div ref="eventsDiv" class="eventsJSON">
            <div v-for="(event, index) in eventLog" :key="index">
                {{ event }}
            </div>
        </div>
        <!-- 渲染容器 -->
        <div style="margin-top:10px;">
            <!-- :layout.sync="layout" 布局数据
            :col-num="12" 栅格一行最多12列
            :row-height="30" 每行高度30
            :is-draggable="draggable" 是否可拖动
            :is-resizable="resizable" 是否可调整大小
            :vertical-compact="true" 垂直布局是否压缩
            :use-css-transforms="true" 使用css属性
            @layout-created="layoutCreatedEvent" vue created生命周期回调
            @layout-before-mount="layoutBeforeMountEvent" vue beforeMount生命周期回调
            @layout-mounted="layoutMountedEvent" vue mounted生命周期回调
            @layout-ready="layoutReadyEvent" 完成mount后回调
            @layout-updated="layoutUpdatedEvent" updated事件回调 -->
            <grid-layout :layout.sync="layout" :col-num="12" :row-height="30" :is-draggable="draggable"
                :is-resizable="resizable" :vertical-compact="true" :use-css-transforms="true"
                @layout-created="layoutCreatedEvent" @layout-before-mount="layoutBeforeMountEvent"
                @layout-mounted="layoutMountedEvent" @layout-ready="layoutReadyEvent" @layout-updated="layoutUpdatedEvent">
                <!-- x 标识栅格元素位于第几列，需为自然数
                y 标识栅格元素位于第几行，需为自然数
                w 标识栅格元素的初始宽度，值为colWidth的倍数
                h 标识栅格元素的初始高度，值为rowHeight的倍数 
                w,h结合所在x,y，不能超出限制的范围，否则位置渲染会有异常
                i 栅格元素id
                @resize="resizeEvent" 调整栅格元素大小回调
                @move="moveEvent" 栅格元素移动回调
                @moved="movedEvent" 栅格元素移动后回调
                @resized="resizedEvent" 调整栅格元素大小后回调
                @container-resized="containerResizedEvent" 栅格元素/栅格容器更改大小的事件（浏览器窗口或其他） -->
                <grid-item v-for="(item, index) in layout" :x="item.x" :y="item.y" :w="item.w" :h="item.h" :i="item.i"
                    @resize="resizeEvent" @move="moveEvent" @resized="resizedEvent"
                    @container-resized="containerResizedEvent" @moved="movedEvent" :key="index">
                    <span class="text">{{ item.i }}</span>
                </grid-item>
            </grid-layout>
        </div>
    </div>
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
            //  可拖拽
            draggable: true,
            //  可变大小
            resizable: true,
            //  无用数据
            index: 0,
            //  事件列表
            eventLog: []
        }
    },
    watch: {
        //  监听事件列表，滚动内容高度
        eventLog: function () {
            const eventsDiv = this.$refs.eventsDiv;
            eventsDiv.scrollTop = eventsDiv.scrollHeight;
        }
    },
    methods: {
        moveEvent: function (i, newX, newY) {
            const msg = "MOVE i=" + i + ", X=" + newX + ", Y=" + newY;
            this.eventLog.push(msg);
            console.log(msg);

        },
        movedEvent: function (i, newX, newY) {
            const msg = "MOVED i=" + i + ", X=" + newX + ", Y=" + newY;
            this.eventLog.push(msg);
            console.log(msg);

        },
        resizeEvent: function (i, newH, newW, newHPx, newWPx) {
            const msg = "RESIZE i=" + i + ", H=" + newH + ", W=" + newW + ", H(px)=" + newHPx + ", W(px)=" + newWPx;
            this.eventLog.push(msg);
            console.log(msg);
        },
        resizedEvent: function (i, newX, newY, newHPx, newWPx) {
            const msg = "RESIZED i=" + i + ", X=" + newX + ", Y=" + newY + ", H(px)=" + newHPx + ", W(px)=" + newWPx;
            this.eventLog.push(msg);
            console.log(msg);

        },
        containerResizedEvent: function (i, newH, newW, newHPx, newWPx) {
            const msg = "CONTAINER RESIZED i=" + i + ", H=" + newH + ", W=" + newW + ", H(px)=" + newHPx + ", W(px)=" + newWPx;
            this.eventLog.push(msg);
            console.log(msg);
        },

        layoutCreatedEvent: function (newLayout) {
            this.eventLog.push("Created layout");
            console.log("Created layout: ", newLayout)
        },
        layoutBeforeMountEvent: function (newLayout) {
            this.eventLog.push("beforeMount layout");
            console.log("beforeMount layout: ", newLayout)
        },
        layoutMountedEvent: function (newLayout) {
            this.eventLog.push("Mounted layout");
            console.log("Mounted layout: ", newLayout)
        },
        layoutReadyEvent: function (newLayout) {
            this.eventLog.push("Ready layout");
            console.log("Ready layout: ", newLayout)
        },
        layoutUpdatedEvent: function (newLayout) {
            this.eventLog.push("Updated layout");
            console.log("Updated layout: ", newLayout)
        },
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

.layoutJSON {
    background: #ddd;
    border: 1px solid black;
    margin-top: 10px;
    padding: 10px;
}

.eventsJSON {
    background: #ddd;
    border: 1px solid black;
    margin-top: 10px;
    padding: 10px;
    height: 100px;
    overflow-y: scroll;
}
</style>