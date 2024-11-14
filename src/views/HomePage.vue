<template>
  <ion-page>
    <ion-content class="ion-padding" style="text-align: center">
      <!-- membuat button get data -->
      <ion-button @click="getData()" style="color: #fff;">Get Data</ion-button>
      <!-- dibuat jika memang terdapat data maka muncul -->
      <table v-if="dataCripto.length>0">
        <thead>
          <th>Name</th>
          <th>Symbol</th>
          <th>Harga Usd</th>
        </thead>
        <tbody>
          <tr v-for="listData in dataCripto" :key="listData.id">
            <td>{{ listData.name }}</td>
            <td>{{ listData.symbol }}</td>
            <td>${{ listData.price_usd}}</td>
          </tr>
        </tbody>
      </table>
      <!-- jika tidak muncul data akan muncul tidak tersedua -->
      <p v-if="toggle">Mohon maaf tidak dapat menampilkan data yang anda inginkan Silakan tekan tombol get data!!!</p>
    </ion-content>
  </ion-page>
</template>

<script>
import axios from "axios";

export default {
  name : "CryptoPage",
  data() {
    return {
      dataCripto:[],
      toggle:false,
    }
  },
  methods: {
    async getData(){
      try{
        const response = await axios.get("https://api.coinlore.net/api/tickers/");
        this.dataCripto = response.data.data;
        if(this.dataCripto.length>0){
          this.toggle = true
        }
      }catch(error){
        console.error("Error while fetching data", error);
        this.toggle = false
      }
    }
  },
};
</script>

<style scoped>
#background-content{
  background-color:#fff ;
}
table{
  width: 100%;
  border-collapse: collapse;
  background-color:#fff ;
}

th{
  border: 1px solid #000;
  padding: 20px;
  background-color:#1a94db ;
  color: #ffffff;
}
td{
  padding: 8px;
  text-align: left;
  color: #000;
}
p{
  color: #000;
}
</style>
