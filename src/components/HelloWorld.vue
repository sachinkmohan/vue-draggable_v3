<template>
    <div style="width:100%;height:3000px;">
       <input type="checkbox" v-model="responsive"/> Responsive 
       <br>
       <input type="text" id="widget" v-model="nameOneCrossOne">
       <button v-on:click="addWidgetItemOneCrossOne">Add Widget Item 1 x 1</button>
       <br>
       <input type="text" id="widget" v-model="nameTwoCrossTwo">
       <button v-on:click="addWidgetItemTwoCrossTwo">Add Widget Item 2 x 2</button>
       <br>
       <input type="text" id="widget" v-model.number="nameRandomX" placeholder="x">
       <input type="text" id="widget" v-model.number="nameRandomY" placeholder="y">
       <input type="text" id="widget" v-model.number="nameRandomW" placeholder="w">
       <input type="text" id="widget" v-model.number="nameRandomH" placeholder="h">
       <input type="text" id="widget" v-model.number="nameRandom" placeholder="enter text">
       <button v-on:click="addRandomWidget">Add Random</button>
        <div style="width:100%;margin-top: 10px;height:100%;">
            <grid-layout :layout.sync="layout"
                        :col-num="4"
                        :row-height="30"
                        :is-draggable="draggable"
                        :responsive="responsive"
                        :vertical-compact="true"
                        :use-css-transforms="true"
            >
                <grid-item v-for="item in layout"
                        :static="item.static"
                        :x="item.x"
                        :y="item.y"
                        :w="item.w"
                        :h="item.h"
                        :i="item.i"
                        :key="item.i"
                >
                    <span class="text">{{itemTitle(item)}}</span>
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
                // {"x":0,"y":0,"w":2,"h":2,"i":"0", static: false},
                // {"x":2,"y":0,"w":2,"h":2,"i":"1", static: false},
                // {"x":0,"y":0,"w":1,"h":1,"i":"2", static: false},
                // {"x":6,"y":0,"w":2,"h":3,"i":"3", static: false},
                // {"x":8,"y":0,"w":2,"h":3,"i":"4", static: false},
                // {"x":10,"y":0,"w":2,"h":3,"i":"5", static: false},
                // {"x":0,"y":0,"w":2,"h":5,"i":"6", static: false},
                // {"x":2,"y":5,"w":2,"h":5,"i":"7", static: false},
                // {"x":4,"y":5,"w":2,"h":5,"i":"8", static: false},
                // {"x":6,"y":3,"w":2,"h":4,"i":"9", static: true},
                // {"x":8,"y":4,"w":2,"h":4,"i":"10", static: false},
                // {"x":10,"y":4,"w":2,"h":4,"i":"11", static: false},
                // {"x":0,"y":10,"w":2,"h":5,"i":"12", static: false},
                // {"x":2,"y":10,"w":2,"h":5,"i":"13", static: false},
                // {"x":4,"y":8,"w":2,"h":4,"i":"14", static: false},
                // {"x":6,"y":8,"w":2,"h":4,"i":"15", static: false},
                // {"x":8,"y":10,"w":2,"h":5,"i":"16", static: false},
                // {"x":10,"y":0,"w":2,"h":2,"i":"17", static: false},
                // {"x":0,"y":9,"w":2,"h":3,"i":"18", static: false},
                // {"x":2,"y":6,"w":2,"h":2,"i":"19", static: false}
            ],
            draggable: true,
            responsive: false,
            index: 0,
            nameOneCrossOne: "",
            nameTwoCrossTwo: "",
            nameRandomX: 0,
            nameRandomY: 0,
            nameRandomW: 0,
            nameRandomH: 0,
            nameRandom: "",

        }
    },
    methods: {
        itemTitle(item) {
            let result = item.i;
            if (item.static) {
                result += " - Static";
            }
            console.log("Responsive value", this.responsive);
            return result;
        },
        addWidgetItemOneCrossOne() {
            if(this.layout.length === 0) {
               this.layout.push({"x":0,"y":0,"w":1,"h":1,"i":this.nameOneCrossOne, static:false}) 
               console.log("After",JSON.stringify(this.layout));
            }
            else {
               let l = this.layout.at(-1); 
               console.log("Before",JSON.stringify(l.x));
            }
            // let l = this.layout.at(-1);
            // console.log("Before",JSON.stringify(l.x));
            // if(l.x != 2){
            // this.layout.push({"x":l.x+2,"y":0,"w":1,"h":1,"i":this.name, static:false})
            //     // l.x = l.x +2;
            // }
            // else {

            // this.layout.push({"x":0,"y":0,"w":1,"h":1,"i":this.name, static:false})
            // }
            // console.log("After",JSON.stringify(l.x));
            // console.log("After",JSON.stringify(l));

        },
        addWidgetItemTwoCrossTwo() {
            if(this.layout.length === 0) {
               this.layout.push({"x":0,"y":0,"w":2,"h":2,"i":this.nameTwoCrossTwo, static:false}) 
               console.log("After",JSON.stringify(this.layout));
            }
            else {
               this.layout.push({"x":1,"y":0,"w":2,"h":2,"i":this.nameTwoCrossTwo, static:false}) 
               console.log("TwoCrossTwo",JSON.stringify(this.layout));
            }
        },
        addRandomWidget(){
            this.layout.push({"x":this.nameRandomX,"y":this.nameRandomY,"w":this.nameRandomW,"h":this.nameRandomH,"i":this.nameRandom, static:false}) 
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
