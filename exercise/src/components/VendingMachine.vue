<template>
  <div>
    <v-card flast>
      <v-row>
        <v-col cols="4" md="2">
        <h3 style=" margin-left: 2rem ; margin-top:3rem; font-size: 22px;">Please insert coins :</h3>
        </v-col>
          <v-col cols="12" md="5">
          <v-card class="mx-5 my-5" width="50%" style="margin-center:">
            <v-row class="text-center">
              <v-col>
                 <v-btn color="warning" fab dark pill variant="primary" class="m-1" @click="insertCoin(1)">
                  1&#3647;
                </v-btn>
              </v-col>
              <v-col>
                <v-btn color="warning" fab dark pill variant="primary" class="m-1" @click="insertCoin(2)">
                  2&#3647;
                </v-btn>
              </v-col>
              <v-col>
                <v-btn color="warning" fab dark pill variant="primary" class="m-1" @click="insertCoin(5)">
                  5&#3647;
                </v-btn>
              </v-col>
              <v-col>
                <v-btn color="warning" fab dark pill variant="primary" class="m-1" @click="insertCoin(10)">
                  10&#3647;
                </v-btn>
              </v-col>
            </v-row>
          </v-card>
      </v-col>
      
      <v-col cols="6" md="5">
          <v-card class="mx-7 my-7" width="80%" style="margin-right">
            <v-row class="text-center">
              <v-card-title>
                 <label>Insert :{{coin}}</label>
                 <label>Total :{{totalCoin}}</label>
                 <label>Change :{{changeCoin}}</label>
                 <label>You get :{{productName}}</label>
                 <v-btn pill variant="outline-primary" @click="refund()">refund</v-btn>
              </v-card-title>
            </v-row>
          </v-card>
        </v-col>
      </v-row>
    </v-card>

    <v-card class="mx-10 my-10">
      <v-row class="mx-10 my-10">
        <template>
          <div v-for="item in product" :key="item.id">
            <v-col>
              <v-card class="mx-auto" max-width="344">
                <v-img :src="item.image" height="200px"></v-img>
                <v-card-title>
                  {{ item.name }}
                </v-card-title>
                <v-card-subtitle> {{ item.price }} &#3647; </v-card-subtitle>
                <v-card-actions>
                   <v-btn
                      text
                     color="green accent-4"
                     @click="pay(item.name,item.price,item.in_stock)"
                    >
                    Buy
                    </v-btn>
                  <v-spacer></v-spacer>
                </v-card-actions>
              </v-card>
            </v-col>
          </div>
        </template>
      </v-row>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: null,
    };
  },
  mounted() {
    this.fetch();
  },
  methods: {
    fetch() {
      this.product = [];
      this.axios
        .get("https://www.mocky.io/v2/5c77c5b330000051009d64c9")
        .then((response) => {
          this.product = response.data.data;
          console.log(response.data);
        })
        .catch((err) => {
          console.log(err.response);
        });
    },
    insertCoin(res){
            this.coin.push(res)
            this.totalCoin = res+this.totalCoin
    },
    pay(name,price,in_stock){
            this.changeCoin = []     
            if(in_stock == true){
                if(this.totalCoin >= price){
                    this.totalCoin = this.totalCoin-price
                    this.remain = this.totalCoin
                    this.productName = name
                while(this.remain >0){
                    if(this.remain >=10){
                        this.changeCoin.push(10)        
                        this.remain = this.remain-10    
                        this.totalCoin = 0
                        this.coin=[]
                    }else if(this.remain >=5){
                        this.changeCoin.push(5)        
                        this.remain = this.remain-5
                        this.totalCoin = 0
                        this.coin=[]
                    }else if(this.remain >=2){
                        this.changeCoin.push(2)        
                        this.remain = this.remain-2
                        this.totalCoin = 0
                        this.coin=[]
                    }else if(this.remain >=1){
                        this.changeCoin.push(1)        
                        this.remain = this.remain-1
                        this.totalCoin = 0
                        this.coin=[]
                    }else{
                        this.remain = 0
                    }
                }        
                }else{
                    this.productName = "not enough money"
                }
            }else{
                this.productName = "out of stock"
            }
        },
        refund(){
            this.changeCoin = this.coin
            this.totalCoin = 0
            this.productName = this.name
            this.coin=[]
        }
  }, 
  data(){
        return{
            coin:[],
            changeCoin:[],
            productName:'',
            remain:0,
            totalCoin:0,
            product:[],
            item:{
                in_stock:Boolean
            }
        }
    },
};
</script>

<style>
.v-btn__content {
    align-items: center;
    color: inherit;
    display: flex;
    flex: 1 0 auto;
    justify-content: inherit;
    line-height: normal;
    position: relative;
    font-size: 20px;
}

</style>