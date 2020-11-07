<template>
    <div>
        <div class="">
            <span>
                    <p class="text">DeFi, envisioned differently.</p>
            </span>
        </div>
        <div class="d-flex justify-content-between mt-5 row" style="">
            <span class="col-10 mt-3 col-md-3 animate__animated animate__backInLeft p-0">
                 <p class="title">Fair</p>
                <p class="sub-title-card">Decentralized Finance started with the belief of ‘banking the unbanked’. <br> <br>
However, to borrow, you need to be overcollateralized and also pay a high APR fee. <br> <br>
This is not suitable to the mainstream. <br> <br>
An alternative model, which is more accessible and financially-friendly for everyone is needed.</p> </span>

            <span class="col-10 mt-3 col-md-3 animate__animated animate__backInRight">
                 <p class="title">Liquidity</p>
                <p class="sub-title-card">Most DeFi tokens follow Bitcoin’s correlation. As liquidity is essential, what will happen when Bitcoin is more bearish?<br> <br>
Currently, we’ve seen DeFi attract liquidity in a semi-bullish market. As this cycle changes, most DeFi protocols will not be sustainable. <br> <br>
Token models designed to be less correlated to Bitcoin would enable liquidity irrespective of the market/bitcoin.</p> </span>
            <span class="col-10 mt-3 col-md-3 animate__animated animate__backInRight" style="margin-bottom: 80px">
                 <p class="title">Non-inflationary</p>
                <p class="sub-title-card">Incentivizing users to participate & offer liquidity is required. Most DeFi protocols issue out large amounts of their own tokens to enable this. <br> <br>
These tokens have one purpose, to be sold by the larger users, creating a high token-velocity, i.e. A highly inflationary design. <br> <br>
Supply-elasticity for rewards would scale DeFi features, and adjust as the demand in the protocol changes.</p></span>
        </div>
        <Menu></Menu>
    </div>
</template>
<script>
  import Menu from './Menu'

  export default {
    name: 'Info',
    components: {
      Menu
    }
  }
</script>

<style scoped>
    .text{
        text-align: center;
        color: #eee;
        font-size: 28px;
    @font-family: Roboto;
    }
    .sub-title-card{
        font-size: 18px;
        color: #eee;
        text-align: left;
        font-weight: 300;

    }
    .title{
        font-weight: 600;
        font-size: 24px;
        color: #eee;
        text-align: center;
    }
</style>
