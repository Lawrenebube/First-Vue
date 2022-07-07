<template>
  <div class="main">
    <div class="calculate">
      <p>BILL</p>
      <div class="input">
        <img :src= "require('../assets/icon-dollar.svg')" alt="dollar" >
        <input 
          :value="bill" 
          @input="updateValue" 
          id="bills"
          type="number">
      </div>
      <p>Select Tip %</p>
      <section class="rates">
        <div @click="calculatePercent(5)" class="rate">5%</div>
        <div @click="calculatePercent(10)" class="rate">10%</div>
        <div @click="calculatePercent(15)" class="rate">15%</div>
        <div @click="calculatePercent(25)" class="rate">25%</div>
        <div @click="calculatePercent(50)" class="rate">50%</div>
        <input v-model="custom" 
         @keyup.enter="customPercent"
          type="number" 
          class="custom" placeholder="Custom">
      </section>
      <p>Number of People <span class="error">{{error}}</span></p> 
      <div class="input">
        <img :src= "require('../assets/icon-person.svg')" alt="$" >
        <input id="people" v-model="person" type="number" >
      </div>
    </div>
    <div class="total-box">
      <section>
        <p>Tip Amount <span class="person">/person</span></p>
        <div>
          <img :src= "require('../assets/icon-dollar.svg')" alt="$" >
          <span class="total">{{personTip || 0.00.toFixed(2)}}</span>
        </div>
      </section>
      <section>
        <p>Total <span class="person">/person</span></p>
        <div>
          <img :src= "require('../assets/icon-dollar.svg')" alt="$" >
          <span class="total">{{total || 0.00.toFixed(2)}}</span>
        </div>
      </section>
      <button @click="reset">RESET</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TipCalculator',
 
  // props: {
    
  // },
 data() {
    return{
     bill:'',
     total:'',
     person:'',
     personTip: '',
     custom:'',
     error: "",
    }
  },
 
  watch: {
    person: function() {
      if (this.person == 0){
        // this.error = "Can't be zero"
        console.log("Can't be zero")
      };    
    },
    custom:function(){
       if (this.custom == 0 || this.custom == ''){
        console.log("no custom value")
      };    
    }
  },
  methods:{
    reset() {
      this.bill = '';
      this.total ='',
      this.person = '';
      this.personTip ='';
      this.custom = '';
      this.error =''
    },
    updateValue(event) {
      const value = event.target.value
      if (String(value).length <= 8) {
        this.bill = value
      }
      this.$forceUpdate()
    },
    checkZero(num) {
      if (this.person == 0){
        this.error = "Can't be zero"
      }
      else {
        this.personTip =`${parseFloat(this.bill*(num/100)/this.person).toFixed(2)}`
      }
    },
    calculatePercent(val) {
      if (this.custom == 0){
        console.log ('no custom')
      }
      else {
        this.checkZero(val);
        this.summation();
      }
    },
    customPercent(){
      if (this.person == 0){
        this.error = "Can't be zero"
      }
      else {
        this.personTip = `${parseFloat(this.bill*(this.custom/100)/this.person).toFixed(2)}`;
        this.summation();     
         }
        
      },
    summation(){
      if (this.person == 0){
        this.error = "Can't be zero"
      }
      else {
        this.total = `${parseFloat(this.bill/this.person).toFixed(2)}`     
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main {
  display: grid;
  grid-template-columns: 1fr 1fr;
  background-color:hsl(0, 0%, 100%) ;
  margin: 20px auto;
  max-width:1000px;
  border-radius: 20px;
}
.calculate {
  background-color:hsl(0, 0%, 100%) ;
  margin: 30px auto;
  padding: auto;
  text-align: left;
  font-size: 14px;
}

  img {
    height: 20px;
    text-align: center;
    justify-content: center;
    margin-top: 6px;
  }
  .calculate p {
    color: hsl(186, 14%, 43%);
  }
  .input {
    display: flex;
    background-color: hsl(189, 41%, 97%);
    justify-content: space-between;
    padding: 10px;
    margin-top: 9px;
    margin-bottom: 10px;
    font-size: 22px;
    border-radius: 7px;
    color: hsl(183, 100%, 15%);
  }

  input {
    background-color: hsl(189, 41%, 97%);
    color: hsl(183, 100%, 15%);
    border:none;
    outline: none;
    text-align: center;
    justify-content: center;
    font-weight: 700;
    font-size: 24px;
  }
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
  }
  .rates{
    font-size: 18px;
    display: grid;
    grid-template-columns: repeat(3,1fr);
    justify-content: center;
    text-align: center;
    gap: 1em;
    color: hsl(0, 0%, 100%);
    margin-bottom: 20px;
    margin-top: 10px;
  }
  .rate{
    background-color: hsl(183, 100%, 15%);
    border-radius:5px ;
    padding: 5px;
  }
  .custom {
    background-color: hsl(189, 41%, 97%);
    color: hsl(184, 14%, 56%);
    max-width: 105px;
    border-radius:5px;
    padding: 9px;
    font-size: 20px;
  }
  .total-box {
    display: grid;
    grid-template-columns: 1fr;
    background-color: hsl(183, 100%, 15%);
    border-radius: 10px;
    justify-content: center;
    text-align: left;
    max-width: 500px;
    padding: 20px 30px 0px 30px;
    margin: 30px ;
  }

  section {
    display: grid;
    grid-template-columns: 1fr 1fr;
    font-weight: 700;
  }

  section p{
    color: hsl(0, 0%, 100%);
    font-size: 14px;
    max-width: 100px;
  }

  section img {
    height: 30px;
    color:hsl(172, 67%, 45%);
  }
  .total {
    color: hsl(172, 67%, 45%);
    font-size: 40px;
    max-width: 50px;
    text-align: center;
    justify-content: center;    
  }
  .person {
    color: hsl(184, 14%, 56%);
  }
  button {
    font-weight: 700;
    font-size: 16px;
    background-color: hsl(172, 67%, 45%);
    padding: 5px;
    border: none;
    outline: none;
    border-radius: 5px;
    max-height: 30px;
    color:hsl(183, 100%, 15%) ;
    margin: 30px auto;
    width: 80%;
  }
  .error{
    margin-left: 85px;
    color: red;
  }

  @media ( max-width:1000px) { 
    .main {
    display: grid;
    grid-template-columns: 1fr ;
    margin: 20px auto ;
    padding-bottom: 30px;
    width:500px;
    }
    .calculate {
    margin: 30px auto;
    padding: auto;
    text-align: left;
    justify-content: center;
  }
  .rates{
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(140px,1fr));
    gap: 1em;
    margin-bottom: 20px;
    margin-top: 10px;
  }
  .custom {
    max-width: 170px;
  }
  .total-box {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1em;
    justify-content: center;
    text-align: center;
    width: 380px;
    padding: 20px 30px 0px 30px;
    margin: 30px auto ;
  }

  button {
    margin: 20px auto 30px auto;
    width: 80%;
  }
}    
</style>
