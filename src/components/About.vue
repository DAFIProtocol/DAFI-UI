<template>
    <div class="container" v-if="loaded && loaded2 && loaded3">
        <div class="d-flex justify-content-around row">
            <div  class="button animate__animated animate__pulse col-12 col-md-4 mt-5">
                <div class="body-button pb-3 " style="padding-left: 15px; padding-right: 15px">
                    <p class="title pb-3">Bitcoin price
                    </p>
                    <p class="sub-title">
                        In the testnet, the volatility of Bitcoin is used to simulate changes in demand/volume, which Datify’s adaptive liquidity-reward system responds to.</p>
                    <p class="title ">${{info.data.amount}}
                    </p>

                </div>
            </div>
            <div  class="button animate__animated animate__pulse col-12 col-md-7">
                <div v-if="isBTC == false">
                        <line-chart :chart-data="datacollection" :height="250" :options="datacollection"></line-chart>
                </div>
                <div v-else>
                        <line-chart-btc :chart-data="datacollectionBtc" :height="250" :options="datacollectionBtc"></line-chart-btc>
                </div>
            </div>
            <div @click="isBTC = !isBTC" class="buttonBTC animate__animated animate__pulse animate__infinite">
                <span  v-if="isBTC == false">DFY</span>
                <span  v-if="isBTC == true">BTC</span>
            </div>
        </div>
        <div class="d-flex justify-content-around row" >
            <div  class="button animate__animated animate__pulse col-12 col-md-4 suply">
                <div class="body-button" style="padding-left: 15px; padding-right: 15px">
                    <p class="title">DFY supply </p>
                    <p class="sub-title">The latest DFY-reward supply, which uses a BTC oracle to adjust based on volume & price. As the demand in DAFI loaning/staking changes, DFY’s availability adjusts accordingly.</p>
                    <p class="title">{{supplyStat[0].price}} DFY</p>
                </div>
            </div>
            <div  class="button animate__animated animate__pulse col-12 col-md-7" style="margin-bottom: 60px">
                <div class="body-button pb-5">
                    <p class="title">DFY wallets
                    </p>
                    <p class="sub-title">Below are the public wallets of DFY testnet tokens.</p>
                    <table style="width:100%" class="sub-title-key" v-if="!isMobile">
                        <tr>
                            <th>Address</th>
                            <th>Last Updated</th>
                            <th>Balance</th>
                        </tr>
                        <hr style="width:200%">
                        <tr v-for="(info,idx) in wallets.slice(0, 3)" :key="idx">
                            <td><a :href="`https://etherscan.io/address/${info.wallet}`">{{info.wallet.substr(0,15)}} ...</a></td>
                            <td>{{info.lastEdit}}</td>
                            <td style="text-align: center">{{info.amount}}</td>
                        </tr>
                        <tr v-for="(infoFull,idx) in wallets.slice(3)" :key="idx" v-if="isVisible">
                            <td><a :href="`https://etherscan.io/address/${infoFull.wallet}`">{{infoFull.wallet.substr(0,15)}} ... </a></td>
                            <td>{{infoFull.lastEdit}}</td>
                            <td style="text-align: center">{{infoFull.amount}}</td>
                        </tr>
                    </table>
                    <ul class="sub-title-key mb-0" v-if="isMobile" >
                        <li v-for="(wallet,idx) in wallets.slice(0, 3)" :key="idx"><a :href="`https://etherscan.io/address/${wallet.wallet}`">{{wallet.wallet}}</a></li>
                    </ul>
                    <ul class="sub-title-key mb-3"  v-if="isVisible && isMobile"  :key="idx">
                        <li v-for="(infoFull,idx) in wallets.slice(3)" :key="idx"><a :href="`https://etherscan.io/address/${infoFull.wallet}`">{{infoFull.wallet}}</a></li>
                    </ul>
                </div>
                <button @click="isVisible = !isVisible" class="buttonMore animate__animated animate__pulse animate__infinite">
                    <span class="glyphicon glyphicon-menu-down" v-if="isVisible == false"></span>
                    <span class="glyphicon glyphicon-menu-up" v-if="isVisible == true"></span>
                </button>
            </div>
        </div>
        <Menu></Menu>
    </div>
    <div class="container" style="text-align: center; margin-top: 10%" v-else>
        <img src="https://www.bluechipexterminating.com/wp-content/uploads/2020/02/loading-gif-png-5.gif" alt="">
    </div>
</template>

<script>/* eslint-disable */
import Menu from './Menu'

  import LineChart from './LineChart.js'
  import LineChartBtc from './LineChartBTC.js'
  import axios from 'axios'
  export default {
    name: 'About',
    components: {
      LineChart,LineChartBtc,Menu
    },
    data () {
      return {
        loaded:false,
        loaded2:false,
        loaded3:false,
        isBTC:false,
        datacollection: null,
        datacollectionBtc: null,
        info:null,
        isVisible: false,
        graph:null,
        supply:[],
        dates:[],
        graphBtc:null,
        supplyBtc:[],
        datesBtc:[],
        isMobile:false,
        wallets:null,
        supplyStat:null,
      }
    },
    mounted() {
      this.checkDevice();
      axios
        .get('https://api.coinbase.com/v2/prices/spot?currency=USD')
        .then(response => (
          this.info = response.data,this.loaded = true
        ))

      axios
        .get('https://europe-west2-majestic-post-289115.cloudfunctions.net/btc-price/addresses')
        .then(response => (this.wallets = response.data.data,this.loaded2 = true))

      axios
            .get('https://europe-west2-majestic-post-289115.cloudfunctions.net/btc-price/supply')
            .then(response => (this.supplyStat = response.data.data,this.loaded3 = true))

      this.fillData()

      setInterval(() =>
      axios
        .get('https://api.coinbase.com/v2/prices/spot?currency=USD')
        .then(response => (this.info = response.data))
        , 3000)
    },
    methods: {
      checkDevice(){
        let screenWitdh = window.screen.width;
         if (screenWitdh <= 765){
           this.isMobile = true;
         }
      },
      fillData () {
        axios
          .get('https://europe-west2-majestic-post-289115.cloudfunctions.net/btc-price/test-supply')
          .then((response) => {
              this.graph = response.data.data
              for (let i in this.graph) {
                this.dates.push(this.graph[i].date)
                this.supply.push(this.graph[i].supply)
              }

              this.datacollection = {
                labels: this.dates,
                datasets: [
                  {
                    label: 'DFY Supply',
                    borderColor: "rgba(0,221,255, 1)",
                    backgroundColor: "rgba(0,221,255, 0.1)",
                    data: this.supply,
                    pointRadius: 0,

                  },
                ],
                options: {
                  responsive: true,
                  maintainAspectRatio: false
                }
              }
            }
          )
        axios
          .get('https://europe-west2-majestic-post-289115.cloudfunctions.net/btc-price/price')
          .then((response) => {this.graphBtc = response.data.data
              for (let i in this.graphBtc){
                this.datesBtc.push(this.graphBtc[i].date)
                this.supplyBtc.push(this.graphBtc[i].price)
              }
            this.datacollectionBtc = {
                labels:this.datesBtc,
                datasets: [
                  {
                    pointRadius: 0,
                    label:'BTC Price',
                    borderColor: "rgba(0,221,255, 1)",
                    backgroundColor: "rgba(0,221,255, 0.1)",
                    data: this.supplyBtc,
                  },
                ],
                options: {
                  responsive: true,
                  maintainAspectRatio: false
                }
              }

            }

          )
      },
    }
  }
</script>
<style scoped>
    @media only screen and (max-width: 769px) {
        .suply {
            padding-right: 20px !important;
            padding-left: 20px !important;
        }
        .sub-title-key {
            font-size: 10px !important;
        }
        .buttonBTC{
            border-radius: 50%;
            height: 40px!important;
            width: 40px!important;
            background: #262625;
            box-shadow: inset 2px 2px 5px rgba(24, 24, 24, 0.5),inset 1px 1px 5px rgba(17, 17, 17, 1);
            border:1px solid #333;
            margin-left: 85%!important;
            margin-top: -190px!important;
            padding-top: 10px !important;
            padding-left: 7.5px !important;
        }
        .buttonBTC span{
            font-size: 12px!important;
            margin-top: 10px;
            color: #eee;
        }
    }
    .button{
        padding: 12px 24px;
        border-radius: 18px;
    }
    .body-button{
        background: #262625;
        box-shadow: inset 2px 2px 5px rgba(34, 34, 34, 0.5),inset 1px 1px 5px rgba(17, 17, 17, 1);
        padding: 12px 28px;
        border-radius: 18px;
        border:1px solid #333;
    }
    .sub-title{
        transition: 2s;
        font-size: 18px;
        color: #eee;
        text-align: left;
    }
    .sub-title-key{
        transition: 2s;
        font-size: 18px;
        color: #eee;
        text-align: left;
    }
    .title{
        font-weight: 600;
        font-size: 24px;
        color: #eee;
        text-align: center;
    }
    .buttonMore{
        border-radius: 50%;
        height: 50px;
        width: 50px;
        background: #262625;
        box-shadow: inset 2px 2px 5px rgba(24, 24, 24, 0.5),inset 1px 1px 5px rgba(17, 17, 17, 1);
        border:1px solid #333;
        margin-left: 43%;
        margin-top: -20px;
    }
    .buttonMore span{
        font-size: 28px;
        margin-top: 8px;
        color: #eee;
    }
    .buttonBTC{
        border-radius: 50%;
        height: 50px;
        width: 50px;
        background: #262625;
        box-shadow: inset 2px 2px 5px rgba(24, 24, 24, 0.5),inset 1px 1px 5px rgba(17, 17, 17, 1);
        border:1px solid #333;
        margin-left: 93%;
        margin-top: -95px;
        padding-top: 13px;
        padding-left: 7.5px;
    }
    .buttonBTC span{
        font-size: 18px;
        margin-top: 10px;
        color: #eee;
    }
    ul{
        padding-left: 20px !important;
    }
    a {
        color: #eee;
    }
    .suply {
        padding-right: 0;
        padding-left: 30px;
    }
</style>
