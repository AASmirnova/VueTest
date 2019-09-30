<template>
  <div class="result-item">
    <input class="result-item__input-reveal" type="checkbox" v-bind:id="id" />
    <label class="result-item__label-reveal" v-bind:for="id">
      <img class="result-item__logo" v-bind:src="result.carrier_logo" v-bind:alt="result.carrier_name"/>
      <span class="result-item__title">{{result.carrier_name}}</span>
    </label>
    <ul class="result-item__offers">
      <li class="result-item__offer" v-for="(item, index) in result.offers" :key="index">
        <div class="result-item__offer-segments" v-for="(segment, index) in item.segments" :key="index">
          <Offer :offer="segment"/>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
    import Offer from './Offer.vue'

    export default {
      name: 'ResultItem',
      components: {
          Offer
      },
      props: {
          result: {
              type: Object,
              required: true
          },
          id: Number
      }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .result-item {
    width: 100%;
    height: 100%;
  }
  .result-item__input-reveal {
    display: none;
  }
  .result-item__label-reveal {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    height: 60px;
    width: 100%;
    position: relative;
    background-color: #fff;
    transition: background-color 0.25s ease;
  }
  .result-item__label-reveal:before {
    content: "+";
    position: absolute;
    font-size: 30px;
    line-height: 30px;
    font-weight: 500;
    right: 40px;
    top: 15px;
  }
  .result-item__offers {
    display: none;
    counter-reset: offers;
  }
  .result-item__input-reveal:checked + .result-item__label-reveal {
    background-color: #f2f2f2;
  }
  .result-item__input-reveal:checked + .result-item__label-reveal:before {
    content: "-"
  }
  .result-item__input-reveal:checked ~ .result-item__offers {
    display: block;
  }
  .result-item__logo {
    height: auto;
    width: auto;
    max-width: 70px;
    margin-left: 40px;
  }
  .result-item__title {
    font-size: 20px;
    font-weight: 600;
    margin: 0 20px;
  }

</style>
