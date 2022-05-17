<template>
    <div class="wrapper-popup" v-bind:class="getClassPopUp">
        <div class="rule">
            <h3>Luật chơi</h3>
            <div class="content-rule" >
                Lorem ipsum, dolor sit amet consectetur adipisicing elit. 
                Sapiente modi dicta quisquam labore quam quas illo ullam alias? 
                Eius, perspiciatis adipisci? Voluptate iste aliquam corrupti libero 
                odio cupiditate reprehenderit dicta.
            </div>
            <button class="confirm" v-on:click="confirm">Đã hiểu</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'pop-up-rule',
    data (){
        return {

        }
    },
    props:{
        activePop: {
            type: Boolean,
            default: false,
        }
    },
    methods: {
        confirm(){
            this.$emit("handleConfirm")
        }
    },
    computed:{
        getClassPopUp: function(){
            return{
                'open-popup': this.activePop
            }
        }
    }
}
</script>

<style>
.wrapper-popup{
    
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgb(162, 147, 147);
    opacity: 0;
    visibility: hidden;
    transition: all .3s ease;
}

.wrapper-popup.open-popup{
    opacity: 1;
    visibility: visible;
}
.rule{
    position: absolute;
    background-color: aliceblue;
    top: 50%;
    left: 50%;
    width: 400px;
    transform: translate(-50%, -50%);
    border: 2px solid rgb(81, 40, 40);
    font-family: Arial, Helvetica, sans-serif;
    padding-left: 10px ;
}

.rule h3 {
    color: blue;
    margin-top: 10px;
}

.rule .content-rule{
    padding-top: 10px;
    padding-bottom: 20px;
}

.rule .confirm{
    padding: 5px 10px;
    border: 1px solid #000;
    cursor: pointer;
    margin-bottom: 10px;
    background-color: aliceblue;
    transition: all .3s ease;
}

.rule .confirm:hover{
    background-color: rgb(158, 183, 205);

}

</style>