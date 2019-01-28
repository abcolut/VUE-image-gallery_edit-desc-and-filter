<template>
<section>
    <img :src ="imgSrc" class="elementImg">
        <br>
     <div @click="showEditor" v-if="flag">{{desc}}</div>
     <div v-if="!flag"><input  v-model="descChange" size=15></input> 
        <button @click="saveDesc">OK</button>
        <button @click="showEditor">Х</button>
     </div>
</section>
</template>

<script>
	export default {
        props: ['imgSrc','desc', 'i'],
        data () {
            return{
                flag: true,
                descChange:null,
            }
        },
		methods:{
            showEditor(){
                this.flag =!this.flag
                this.descChange = this.desc
            },
            saveDesc(){
                this.flag =!this.flag
                this.$emit('changeDesc', {i:this.i , desc:this.descChange});
                this.flagNewImage=true
            }
        },
    };


</script>

<style scoped>

section{    
    margin:10px;
    padding:10px;
    border:1px solid #def1fe;
}
img{
    height:150px;
}
    
</style>