<template>
 <div class="flex flex-col flex-initial items-center">
    <button class="hover:bg-blue-700 text-[20px] mt-10 text-white uppercase bold mb-10 py-5 px-5 border rounded-md border-solid border-black bg-blue-500"  @click="fetchShop(), fetchName()">Generate Dog</button>
    <img class="w-[400px] h-[400px] rounded-md border-2 border-solid border-black" v-if="image&&name!==nametemp" :src="image" alt="">
    <h1 class="text-[40px] text-center">{{name[0]}}</h1>
  </div> 
</template>
<script>
import "@/assets/tailwind.css"

export default{
    data(){
        return{
          url_base:"https://dog.ceo/api/breeds/image/random", 
          dog: {},
          image:"",
          name_url:"https://random-word-api.herokuapp.com/word?lang=it",
          name:"",
          nametemp:"placeholder",
        }
      },
      methods:{
        fetchShop(){
          this.name="";
          fetch(this.url_base)
          .then(res=>{
            return res.json();
          }).then(this.setResults);
        },
        fetchName(){
          fetch(this.name_url)
          .then(res=>{
            return res.json();
          }).then(this.setName).then(this.nametemp=this.name);
        },
        setResults(results){
          this.dog=results;
          this.image=this.dog.message;
        },
        setName(name){
          this.name=name;
        },
        
  }
}

</script>
