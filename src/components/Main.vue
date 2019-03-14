<template>
    <div>
        <ul>
            <li v-for="(item,index) in myResearchContent[1  ]" :key="index">
                <h2>{{index+1}}. {{item}}</h2>
                <p>{{myResearchContent[2][index]}}</p>
                <a>{{myResearchContent[3][index]}}</a>
            
            </li>
        </ul>
    </div>
</template>

<script>
import {bus} from './event.js';

let globalContent= []

export default{
    props:{
    },
    data(){
        return{
            obtainedText: 'ContentPlaceHolder',
            myResearchContent: []
        }
    },
    mounted(){
        
            bus.$on('textentered', data=>{
                this.updateRecherche(data)          
            })
        
    },
    methods:{
        
        updateRecherche :  function(recherche){
            let request = new XMLHttpRequest();
            let URL = "https://cors-anywhere.herokuapp.com/https://en.wikipedia.org/w/api.php?action=opensearch&format=json&search=";
            let safeTextRequest = encodeURI(recherche)

            let myRequest = request.open('GET',URL+safeTextRequest,true);
            console.log(URL+safeTextRequest)    
            request.onload= function(e){
                if(request.readyState==4 && request.status==200){
                    request.responseText
                    globalContent =JSON.parse(request.responseText)
                    this.myResearchContent= globalContent
                    console.log(globalContent)
                } else{
                    this.myResearchContent =  'A problem occured while loading'
                }
            }
            request.send()            
            this.myResearchContent= globalContent
            console.log(this.myResearchContent)
        }
    }  
}


</script>

<style scoped>
div{
    background:none;
    display: inline;
    position: relative;
}
</style>
