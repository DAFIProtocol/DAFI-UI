<template>
  <div class="">
    <p class="text">
        Datify is an elastic, zero-fee DeFi protocol, which innovatively <br> combines lending, staking and elasticity. Making DeFi truly accessible.</p>
    <div class="d-flex justify-content-center">
      <router-link :to="`/about`"  class="button animate__animated animate__pulse animate__infinite">
        <div class="body-button">
          <p class="title">Enter</p>
          <p class="sub-title">Click here to use the DAFI v1.0 MVP</p>
        </div>
      </router-link>
    </div>
    <div class="d-flex justify-content-between mt-5 row " >
            <span class="col-12 mt-3 col-md-5 animate__animated animate__backInLeft">
                 <p class="title">What is Datify?</p>
                 <p class="sub-title-card">Datify is the first DeFi project incubated  by a CeFi bank, with the vision to make DeFi more accessible. This is enabled via a combination of lending & staking to eliminate fees entirely. Read the Litepaper for more.</p>
            </span>

      <span class="col-12 mt-3 col-md-5 animate__animated animate__backInRight" style="margin-bottom: 60px">
                 <p class="title">How does it work?</p>
                 <p class="sub-title-card">When DAFI tokens are loaned, they are staked to issue supply-elastic DFY’s. This incentivizes liquidity without borrowers paying high fees. As the demand in the DAFI protocol changes, the DFY volume adjusts the supply proportionally. Datify is a system that is adaptive to it’s demand, and designed to achieve liquidity without correlating to Bitcoin. A sustainable, fair economy.</p>
      </span>
    </div>
    <Menu></Menu>
  </div>
</template>

<script>
import Menu from './Menu'
export default {
  name: 'Home',
  components: {
    Menu
  },
  data () {
    return {

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .text{
    text-align: center;
    color: #eee;
    font-size: 28px;
  @font-family: Roboto;
  }
  .button{
    margin-top: 10%;
    padding: 12px 24px;
    border: 1px solid #134e62;
    border-radius: 18px;
  }
  .body-button{
    background: #262625;
    box-shadow: inset 2px 2px 5px rgba(34, 34, 34, 0.1),inset 1px 1px 5px rgba(17, 17, 17, 1);
    text-align: center;
    padding: 12px 28px;
    border: 1px solid #0292c6;
    border-radius: 18px;
  }
  .sub-title{
    font-size: 18px;
    color: #eee;
    text-align: center;
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
