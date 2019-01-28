<template>
<section>
    <hr>
	<div>
		Внесение изображения в галлерею:
	    <div v-if="flagNewImage">
            <input type="file" @change="previewThumbnail"  accept="image/*">
        </div>
		<div v-if="!flagNewImage"> 
			<img height="100px" :src="src" >
			<br><br><input  v-model="ImageName" size=15></input> 
			<br><br><button @click="imageComplete()">Готово</button>
		</div>
	</div>
</section>
</template>

<script>
	export default {
        data () {
            return {
                content: null,
                file: null,
                isLoading: false,
                flagNewImage:true,
                ImageName:'name',
            }
        },
		computed: {
            events () {
                return {IMAGE_CHANGED: 'image-changed'};
            },
            src () {
                if (this.content) {
                    return this.content;
                }
                return this.isEmpty ? '' : this.srcPrefix + this.value;
            },
		},
		methods:{
			previewThumbnail (event) {
                this.handleFiles(event.target.files)
            },
            handleFiles (files) {
                if (!files || !files[0]) {
                    return;
                }
                if (!/^image\//.test(files[0].type)) {
                    return;
                }
                this.selectImage(files[0]);
            },
            selectImage (file) {
                let reader = new FileReader();
                reader.onload = this.onImageLoad;
                this.isLoading = true;
                this.file = file;
                reader.readAsDataURL(file);
            },
            onImageLoad (e) {
                this.content = e.target.result;
                this.isLoading = false;
                let filename = this.file instanceof File ? this.file.name : '';   
                this.flagNewImage = false   
            },
			imageComplete(){
            	this.$emit('newImage', {imgSrc:this.content , desc:this.ImageName});
            	this.flagNewImage=true
			},       
        },	
    };


</script>

<style scoped>
section{
	#border: 1px solid gray;
	padding:10px;
}
</style>