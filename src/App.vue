
<template>
  <transition name="dissolve">
    <Modal @closedModal="modalOpen = false" :products="products" :selected="selected" :modalOpen="modalOpen"/>
  </transition>

  <nav class="upper-menu">
    <div class="upper-nav">
      <a v-for="m in menus" :key="m" href="#" aria-label="{{m}}">{{m}}</a>
    </div>
  </nav>

  <Flexible v-if="showFlexible == true" />

  <!-- <div class="product-list"> -->
      <!-- <a href="#">
        <h4 v-for="(prd,i) in products" :key="i">
          {{ prd }}
        </h4>
      </a>
      <p v-for="(prc,i) in prices" :key="i">
        €{{ prc }}
      </p> -->

  <div class="filter-button">
    <button @click="priceSort">
    View by price
    </button>
    <button @click="reset">
      Reset the filter
    </button>
  </div>


  <div class="product-list">
    <Card @click="modalOpen = true; selected = i" :product="products[i]" v-for="(a,i) in products" :key="i" />
  </div>
    <!-- <Card :product="products[1]" />
    <Card :product="products[2]" />
    <Card :product="products[3]" />
    <Card :product="products[4]" />
    <Card :product="products[5]" /> -->

    <!-- <div class="product" v-for="(name,i) in products" :key='i'>
      <img :src="products[i].image" alt="product 1" class="product-image" />
      <h4 @click="modalOpen = true; selected = i">{{ products[i].title }}</h4>
      <p>€{{ products[i].price }}</p>
      <div class="like-count">
      <button @click="likes[0] ++">Likes</button>
      <span>{{likes[0]}}</span>
    </div>  -->
  <!-- <nav class="lower-menu">
    <a href="#" class="lower-menu-1">
      <div class="icon-explore">
        <svg viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" role="presentation" focusable="false" style="display: block; fill: none; height: 24px; width: 24px; stroke: currentcolor; stroke-width: 4; overflow: visible;">
          <g fill="none">
            <path d="m13 24c6.0751322 0 11-4.9248678 11-11 0-6.07513225-4.9248678-11-11-11-6.07513225 0-11 4.92486775-11 11 0 6.0751322 4.92486775 11 11 11zm8-3 9 9">
            </path>
          </g>
        </svg>
      </div>
      <p class="lower-menu-1-text">
        Explore
      </p>
    </a>
    <a href="#" class="lower-menu-2">
      <div class="icon-like">
        <svg viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" role="presentation" focusable="false" style="display: block; height: 24px; width: 24px; fill: currentcolor;">
          <path d="m23.0204313 3.00582063c-2.0815427.07751293-4.0715877.92728952-5.5789504 2.43470494l-1.4414809 1.44047443-1.4404171-1.44031065c-1.5845115-1.58335003-3.6983863-2.44068935-5.8929929-2.44068935-2.19416638 0-4.30898823.85772467-5.89177678 2.44051322-1.58391215 1.58390109-2.44156322 3.69775756-2.44156322 5.89278678 0 4.9282095 2.48419629 8.8512108 8.03256412 13.439053l.70954716.5770638.74171734.584714.77413928.5930892c.131739.0995864.2648394.199552.3993065.2999118l.823244.607011.8562953.6171982.8895983.6281103.9231529.6397472 1.5170817 1.0308345 1.3291121-.9009656 1.0589072-.7287753.6612652-.4625621.7010987-.498181.8533598-.6198244c7.3971739-5.4452801 11.0629604-10.1222564 11.0629604-15.8064246 0-2.19559863-.8569151-4.30921968-2.4404957-5.89278925-1.5843319-1.58317036-3.6982062-2.44051075-5.8928043-2.44051075zm.3128687 1.99417937c1.6695137 0 3.2735403.65055751 4.4788526 1.85498605 1.2043504 1.20434208 1.8544474 2.80783678 1.8544474 4.47831395 0 4.2987547-2.6123854 8.1213061-8.009061 12.474023l-.7197183.570835c-.2451788.1913357-.495635.3837563-.7513829.5773445l-.7831323.5843503-.8149664.5918523-.6943428.4933793-.6495182.4543204-1.2444781.8545952-.3599806-.2464089c-.3060116-.2102151-.6062613-.4182535-.900798-.6242279l-.8665202-.6118437c-.1415799-.1009795-.2817437-.2014711-.4204976-.3014889l-.8156535-.594534c-.1331387-.0981789-.2648797-.1959122-.3952291-.2932139l-.7654464-.5787439-.7323414-.5690616c-5.8464087-4.609638-8.4102832-8.3182024-8.4102832-12.7811772 0-1.66972745.65069601-3.27350087 1.85577431-4.47857075 1.20389067-1.20389067 2.80861035-1.85472925 4.47756569-1.85472925 1.6695226 0 3.2735495.6505567 4.4788626 1.85498605l2.8542663 2.8556887 2.8559829-2.85594303c1.2038387-1.20388075 2.8086117-1.85473172 4.4775982-1.85473172z">
          </path>
        </svg>
      </div>
      <p class="lower-menu-2-text">
        Wishlists
      </p>
    </a>
    <a href="#" class="lower-menu-3">
      <div class="icon-user">
        <svg viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" role="presentation" focusable="false" style="display: block; height: 24px; width: 24px; fill: currentcolor;">
          <path d="m16 1c8.2842712 0 15 6.71572875 15 15 0 8.2842712-6.7157288 15-15 15-8.28427125 0-15-6.7157288-15-15 0-8.28427125 6.71572875-15 15-15zm0 8c-2.7614237 0-5 2.2385763-5 5 0 2.0143973 1.2022141 3.7998876 2.9996346 4.5835001l.0003231 2.0984999-.1499943.0278452c-2.8326474.5613112-5.31897338 2.2230336-6.93575953 4.5872979 2.34343054 2.291067 5.54974273 3.7028569 9.08579613 3.7028569 3.5355506 0 6.7414538-1.4113884 9.0850203-3.701476-1.6141801-2.3628535-4.0978119-4.0247647-6.929184-4.5867938l-.1558786-.0287302.001228-2.0991413c1.7288399-.7547474 2.9066959-2.4357565 2.9936498-4.355479l.0051645-.2283797c0-2.7614237-2.2385763-5-5-5zm0-6c-7.17970175 0-13 5.82029825-13 13 0 2.9045768.95257276 5.5866683 2.56235849 7.7509147 1.42074739-1.9134907 3.33951478-3.4002416 5.53860831-4.2955956l.3480332-.1363191-.0229565-.0189706c-1.43704227-1.2411241-2.34462949-3.045583-2.42083359-5.0285539l-.00520991-.2714755c0-3.8659932 3.1340068-7 7-7s7 3.1340068 7 7c0 1.9941317-.8415062 3.8279876-2.224566 5.1193683l-.225434.2006317.0447787.0163138c2.3268368.8792152 4.3570558 2.4138611 5.8430586 4.4127726 1.6098837-2.1632453 2.5621627-4.8449575 2.5621627-7.7490864 0-7.17970175-5.8202983-13-13-13z">
          </path>
        </svg>
      </div>
      <p class="lower-menu-3-text">
        Log in
      </p>
    </a>
  </nav> -->
</template>

<script>

import data from './assets/vuerbnb';
import Flexible from './components/Flexible.vue';
import Modal from './components/Modal.vue';
import Card from './components/Card.vue';

export default {
  name: 'App',
  data() {
    return {
      showFlexible: true,
      selected: 0,
      productsOriginal:[...data],
      products: data,
      modalOpen: false,
      menus: ['Explore', 'Experiences', 'Filter'],
      // links: ["https://bit.ly/3fkHwrF", "https://bit.ly/3lm9c3a", "https://bit.ly/3jfBLwm"],
      // likes: [0,0,0],
    }
  },

  mounted() {
      setTimeout(()=> {
        this.showFlexible = false;
      }, 2000);
    },
  components: {
    Flexible,
    Modal,
    Card,
  },
  methods: {
    increase(){
      this.likes += 1;
    },

    reset() {
    this.products = [...this.productsOriginal];
    },

    priceSort() {
      this.products.sort(function(a,b){
        return a.price - b.price
      }) 
    },
  }
}
</script>

<style>
/* transitions from here */
.dissolve-enter-from {
  opacity: 0;
  /* transform: translateY(-10000px); */
}
.dissolve-enter-active {
  transition: all ease-in-out 250ms;
}
.dissolve-enter-to {
  opacity: 1;
  /* transform: translateY(0px); */
}

.dissolve-leave-from {
  opacity: 1;
}
.dissolve-leave-active {
  transition: all ease-in-out 250ms;
}
.dissolve-leave-to {
  opacity: 0;
}
/* transitions to here */
* {
  box-sizing: border-box;
  margin: 0;
  font-family: 'DM Sans', sans-serif;
}

a {
  text-decoration: none;
  color: #000;
}

button {
  border: none;
  background-color: transparent;
}

.upper-nav {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin-bottom: 80px;
  padding: 8px 42px;
  height: 80px;
  color: hsl(0 0% 13%);
  background-color: #fff;
  box-shadow: 0px 4px 5px rgba(99, 99, 99, 0.14), 0px 1px 10px rgba(99, 99, 99, 0.12), 0px 2px 4px rgba(99, 99, 99, 0.2);
}

.upper-nav a {
  margin-right: 42px;
  color: #222;
}

.upper-nav a:last-child {
  margin-right: 0;
}

/* .like-count {
  display: flex;
  justify-content: center;
  align-items: center;
}

.like-count button {
  border: none;
  border-radius: 2px;
  margin-right: 8px;
  padding: 4px 11px;
  font-weight: 700;
  color: #fff;
  background-color: #FF385D;
} */

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}


.filter-button button {
    border-radius: 4px;
    margin: 0 42px 42px 0;
    padding: 11px 23px;
    font-weight: 700;
    color: #F3EED9;
    background-color: #2F4858;
}

.filter-button button:last-child {
  margin-right: 0;
}

.product-list {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

</style>
