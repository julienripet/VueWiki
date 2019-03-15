<template>
    <div id="articles">
        <ul>
            <li id="articleIndividuel" v-for="(item,index) in myResearchContent[1]" :key="index">
                <h2>{{index+1}}. {{item}}</h2>
                <p v-on:click="snipping(index)" v-if='myResearchContent[4][index]' >{{myResearchContent[2][index]|snippet}}</p>
                <p v-on:click="snipping(index)" v-if='!myResearchContent[4][index]' >{{myResearchContent[2][index]}}</p>
                <a v-bind:href="myResearchContent[3][index]">{{myResearchContent[3][index]}}</a>
            
            </li>
        </ul>
    </div>
</template>

<script>
import {bus} from './event.js';

export default{
    props:{
    },
    data(){
        return{
            snip:true,
            snipped:[],
            obtainedText: 'ContentPlaceHolder',
            myResearchContent: ['',[],[],[],[]]
        }
    },
    created(){
        
            bus.$on('textentered', data=>{
                this.updateRecherche(data)          
            })
        
    },
    methods:{
        snipping: function(i){
            //this.snip=!this.snip
            this.myResearchContent[4][i]=!this.myResearchContent[4][i]
            console.log(this.myResearchContent[4])
            this.$forceUpdate()
        },

        updateRecherche :  function(recherche){
            let request = new XMLHttpRequest();
            let safeTextRequest = encodeURI(recherche)
            this.$http.get("https://cors-anywhere.herokuapp.com/https://en.wikipedia.org/w/api.php?action=opensearch&format=json&search=" + safeTextRequest).then(function(data){
                this.myResearchContent = data.body
                for(let i=0;i<this.myResearchContent[1].length;i++){
                    this.snipped[i] = true
                }
                console.log(this.snipped)
                this.myResearchContent.push(this.snipped)
                console.log(this.myResearchContent)

            })
        }
    }  
}


</script>

<style scoped>
#articles{
    max-width: 900px;
    margin:20px auto;
    /* background-color: lightgray; */
    padding:20px;
    border-radius: 5px;
}
ul{
    padding:0;
}
li{
    list-style: none;
}
#articleIndividuel{
    /* border:1px solid rgb(88, 88, 88); */
    margin:15px;
    padding:10px;
    border-radius: 15px;
    background-color: #eee;
}
</style>
