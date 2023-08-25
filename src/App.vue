<script setup>
import { ref, reactive, computed } from "vue";
import ParentComponent from "./components/ParentComponent.vue";
import ChildComponent from "./components/ChildComponent.vue";

const variants = reactive([
  { id: 1, name: "Vanilla", price: 100 },
  { id: 2, name: "Chocolate", price: 120 },
  { id: 3, name: "Strawberry", price: 90 },
  { id: 4, name: "Orange", price: 70 },
  { id: 5, name: "Lemon", price: 30 },
]);

let cart = ref([]);

const addToCart = (variantId) => {
  cart.value.push(variants.find((variant) => variant.id === variantId));
};

const removeFromCart = (variantId) => {
  const position = cart.value.findIndex((variant) => variant.id === variantId);
  cart.value.splice(position, 1);
};

const total = computed(() => {
  return cart.value.reduce((total, variant) => total + variant.price, 0);
});

const showModal = ref(false);

const toggleModal = () => {
  showModal.value = !showModal.value;
};
</script>

<template>
  <!-- header start -->
  <header>
    <div class="container" id="header">
      <div>
        <img class="logo" src="images/logo.svg" alt="Logo" />
      </div>
      <div class="textRight">
        <img src="images/vue.svg" alt="Vue.js" class="vueLogo" /><strong
          >Vue.js</strong
        >
      </div>
    </div>
  </header>
  <!-- header end -->

  <!-- body start -->
  <div class="mainBody" id="body">
    <div class="container" id="iceCreamBuilder">
      <!-- icecream start -->
      <ParentComponent :cart="cart" />
      <!-- ice cream end -->
      <!-- builder start -->
      <div id="builder">
        <div class="builder">
          <h3>
            Build your cool Ice Cream
            <span
              class="quantity"
              :style="cart.length === 0 ? { color: 'red' } : {}"
              >{{ cart.length }}</span
            >
          </h3>
          <!-- items start -->

          <div id="items">
            <ul>
              <!-- item start -->
              <li class="item" v-for="variant in variants" :key="variant.id">
                <span>{{ variant.name }}</span>
                <div class="right">
                  <button
                    type="button"
                    class="plus rounded"
                    @click="addToCart(variant.id)"
                  >
                    +
                  </button>
                  <button
                    type="button"
                    class="minus rounded"
                    @click="removeFromCart(variant.id)"
                  >
                    -
                  </button>
                </div>
              </li>
              <!-- item end -->
            </ul>
          </div>
          <!-- items end -->

          <!-- total price start -->
          <div class="total" id="total">
            <div>Total Price</div>
            <div>{{ total }} Tk</div>
          </div>
          <!-- total price end -->
          <button type="button" class="order rounded" @click="toggleModal">
            Proceed
          </button>
        </div>

        <!-- modal start -->
        <ChildComponent
          v-model="total"
          v-show="showModal"
          @message-emitted="toggleModal"
        />
        <!-- modal end -->
      </div>
      <!-- builder end -->
    </div>
  </div>
  <!-- body end -->

  <!-- footer start -->
  <footer>
    <div class="container" id="footer">
      <div>Copyright &copy;2020.</div>
      <div class="textRight">
        Built with <span class="red">&hearts;</span> by
        <a href="#" target="_blank">SM Emon Islam</a>
      </div>
    </div>
  </footer>
  <!-- footer end -->
</template>

<style scoped></style>
