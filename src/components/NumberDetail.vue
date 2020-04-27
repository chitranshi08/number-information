<template>
  <div>
  		<h1>Interesting Fact About Numbers</h1>

  	<div class="mainContainer">
 <input type="text"  @keyup.enter="getResult"  v-model="enterNumber" @input="hideText" placeholder="Please enter any number" />
 <div v-if="result" class="container">
 	<div>{{numberFact}}</div>
 </div>
</div>
<div v-show="showLoader" class="loader">
          <img src="../assets/loader.gif" alt="">
        </div>
  </div>
</template>

<script>
export default {
  name: 'NumberDetail',

  data:()=>({
enterNumber:null,
numberFact:null,
result:false,
showLoader:false
  }),
methods:{
getResult(){
	var number = this.enterNumber 
	this.showLoader = true;
fetch(`https://numbersapi.com/${number}?json`)
.then((response)=>{return response.json()})
.then((response)=>{
	console.log(response)
	this.numberFact = response.text
})
.finally(()=>{
	this.showLoader = false
	this.result = true

})
},
hideText(){
	this.result = false
}

}
}
  
  

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mainContainer{
	width:100vw;
	height: 100px;
	color:white;
}
.container{
	height: 100px;
	font-weight: bold;
	font-size:30px;
}
input{
	margin-bottom: 30px;
	width:150px;
	padding:10px;
}
.loader{
  height: 100vh;
  width:100vw;
  position: fixed;
  top:0;
  left:0;
  background-color: rgba(255,255,255,0.6);
  display: flex;
  justify-content: center;
  align-items: center;

}

</style>