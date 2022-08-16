<template>
  <div class="container">
    <div class="info-container">
      <div class="header">
        
      </div>
      <div class="prices-container">
          <div class="price">
            <label for="">DolarToday </label>
            {{priceDolar}}
            Bs
          </div>
          <div class="price">
            <label for="">Dolar BCV </label>
            {{priceDolarBcv}}
            Bs
          </div>
          <div class="price">
            <label for="">Euro </label>
            {{priceEuro}}
            Bs
          </div>
      </div>
          <div class="fecha">
            {{fecha}}
          </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'

export default{
  data(){
    return{
      priceDolarBcv:null,
      priceDolar:null,
      priceEuro:null,
      fecha:null,
    }
  },
  methods:{
    async getData(){
      let dataDolar= await axios.get('https://s3.amazonaws.com/dolartoday/data.json');
      console.log(dataDolar.data._timestamp.fecha)
      this.priceDolar= await dataDolar.data.USD.dolartoday
      this.priceDolarBcv= await dataDolar.data.USD.sicad2
      this.priceEuro= await dataDolar.data.EUR.dolartoday
      this.fecha= await dataDolar.data._timestamp.fecha
    }
  },
  created(){
    this.getData()
  }

}

</script>
<style>
*{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-size: 16px;
}

.container{
  width:100%;
  margin: 0 auto;
  height: 100vh;
  display:flex;
  justify-content: center;
  align-items: center;
}
.info-container{
  width: 60%;
  min-height: 600px;
  background-color: #fcfcfc;
  border-radius: 6px;
  box-shadow: 5px 5px 4px rgba(0, 0, 0, 0.226);
  position: relative;
}
.header{
  width: 100%;
  height: 80px;
  background-color: #32a332;
  border-radius: 6px 6px 0 0;
}
.prices-container{
  width: 100%;
  height: 480px;
  display: flex;
  gap: 2em;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.price{
  display: flex ;
  flex-direction: column;
  align-items: center;
  gap:.5em;
  font-size: 1.4em;
  width: 90%;
}
.price label{
  font-size: 2em;
  background-color:rgba(50, 163, 50, 0.698);
  display:inline-block;
  width: 80%;
  border-radius: 6px;
}
.fecha{
  position: absolute;
  right: 20px;
  bottom: 20px;
}
</style>
