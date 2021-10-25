<template>
<div class="gameArea">
    <img alt="Vue logo" src="../assets/logo.png">

    <h3>{{result}}</h3>
    <h4>Current Box: {{currVal}}</h4>
    <div class="boxHolder">
        <div class="box"
            v-for="(box, index) in boxData" :key="index"
            >
            <button
                :class="box.show ? 'show' : '' "
                @click="showBox(index, box.value )">
                <p v-if="!box.show">Click Here</p>
                <span>{{box.value}}</span>
            </button>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: "MemoryGame",
    data() {
     return {
        boxData: [
            { id:1, value: "🍊", show: false },
            { id:2, value: "🍎", show: false },
            { id:3, value: "🍎", show: false },
            { id:4, value: "🍊", show: false },
            { id:5, value: "🍰", show: false },
            { id:6, value: "🍩", show: false },
            { id:7, value: "🍩", show: false },
            { id:8, value: "🍰", show: false }
        ],
        currVal: null,
        result: ''
     }
    },
    methods: {
        showBox( _id, _value ){

            console.log("Values: ", this.currVal , _value);

            this.boxData[_id].show=true;
            
            if( this.currVal === null ) {
                this.currVal=_value;
            }else if( _value===this.currVal) {
                this.result = "Great!"
                this.currVal=null;
            } else {
                this.result = "Try again!"
                this.boxData.map( box=>  box.show=false )
                this.currVal = null
            }
        }
    }
}
</script>

<style scoped>
*{
    transition: all 0.5s;
}
.gameArea {
    width: 100%;
    float: left;
}
.boxHolder {
    display: block;
    width: 800px;
    margin: 0 auto;
}
.box { 
    width: 200px; 
    float: 
    left; 
}
button p {
    margin-top: 46px; 
    margin-bottom: 0;
}
button.show p {  
    margin: 0;  
}
.box button { 
    width: 100%; 
    height: 100px;
    border: 1px solid #ddd;
    border-radius: 0;
}
.box button span { 
    font-size: 50px; 
    opacity: 0;
}
button.show {
    background: #dcf7eb;
    box-shadow: 0 0 0px 2px #41b883;
    position: relative;
}
.box button.show span { 
    opacity: 1;
}
</style>