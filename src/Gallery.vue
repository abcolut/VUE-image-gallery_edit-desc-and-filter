<template>
<section>
    <hr>
    <div>
        Фильтр записей: <input  v-model="filtr" size=15> {{count}}
    </div>

    <newImage @newImage="newImage"></newImage>
    
    <hr>

    <div v-for="flagShow,i of doGalleryWidthFilter()" class="element"> 
        <picDesc v-if=" flagShow > -1 "
            :desc="gallery[i].desc"
            :imgSrc="gallery[i].imgSrc"
            :i = "i"
            @changeDesc = "changeDesc"
        > </picDesc>
    </div>
<hr>
<p>Описание задания и работы алгоритма:</p>

<h3> Приложение  "Галлерея" </h3>
<p>Должна быть возможность добавить новое изображение в галерею. По нажатию на кнопку выбираем файл, далее указываем название картинки. После чего он добавляется в галерею и картинка сразу рендерится. (На сервер картинка не выгружается)</p>
<p>Сама галерея представляет собой таблицу из картинок и их названий внизу. Таблица автоматически уменьшается под размер экрана.</p>
<p>По клику на название картинки, можно его там же отредактировать.</p>
<p>Вверху страницы реализовать поиск по названию, при вводе должны отображаться только те картинки чье название содержит введенное значение. При очистке этого поля все картинки снова отображаются. Рядом с поиском отображается количество найденных записей.</p>

<a href=https://krasnodar.hh.ru/resume/0e8113cdff026319990039ed1f4534786d6e65> ссылка на резюме - ищу работу VUE программиста </a>

</section>
</template>

<script>
    import newImage from "./Images.vue";
    import picDesc from "./Desc.vue";
	export default {
        components:{newImage, picDesc }, 

        data () {
            return{
                gallery:[],
                filtr:"",
                count:0,                
            }
        },
		methods:{	
            doGalleryWidthFilter(){
                var filtr_ = this.filtr               
                var res =[]
                for (var i=0; i< this.gallery.length; i++){
                    var flag = this.gallery[i].desc.indexOf(this.filtr)
                    //if (this.gallery[i].desc.indexOf(this.filtr)!==-1){
                        res.push(flag)               
                    //}
                }
                this.count = res.length
                return res
            },
            src(i){ 
                return this.gallery[i].imgSrc
            },
            changeDesc(data){
                this.gallery[data.i].desc = data.desc
            },
            newImage(e){
                this.gallery.push(e)
            }
        },	
    }


</script>

<style scoped>
.element{
    display: inline-block;
    #margin:10px;
    #padding:10px;
    #border:1px solid #def1fe;
}
.elementImg{
    width:150px;
}

</style>