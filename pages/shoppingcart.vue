<template>
  <MainLayout>
    <section id="ShoppingCartPage" class="mt-4 max-w-[1200px] mx-auto px-2">
      <div v-if="false" class="h-[500px] flex items-center justify-center">
        <div class="pt-20">
          <img src="/cart-empty.png" width="250" alt="cart-empty" />

          <div class="text-xl text-center mt-4">No items yet?</div>

          <div v-if="true" class="flex text-center">
            <NuxtLink
              to="/auth"
              class="bg-[#fd374f] w-full text-white text-[21px] font-semibold p-1.5 mt-4 rounded-full"
            >
              Sign In
            </NuxtLink>
          </div>
        </div>
      </div>

      <div v-else class="md:flex gap-4 justify-between mx-auto w-full">
        <div class="md:w-[65%]">
          <div class="bg-white rounded-lg p-4">
            <div class="text-2xl font-bold mb-2">Shopping Cart (0)</div>
          </div>

          <div class="bg-[#feeeef] rounded-lg p-4 mt-4">
            <div class="text-red-500 font-bold">
              Wellcome Deal applicable on 1 item only
            </div>
          </div>

          <div class="bg-white rounded-lg p-4 mt-4">
            <div v-for="product in products">
              <CartItem
                :product="product"
                :slectedArray="selectedArray"
                @selectedRadio="selectedRadioFunc"
              />
            </div>
          </div>
        </div>

        <div class="md:hidden block my-4" />

        <div class="md:w-[35%]">
          <div class="bg-white rounded-lg p-4">
            <div class="text-2xl font-extrabold mb-2">Summary</div>
            <div class="flex items-center justify-between my-4">
              <div class="font-semibold">Total</div>
              <div class="font-semibold text-2xl">
                $ {{ totalPriceComputed }}
              </div>
            </div>

            <button
              @click="goToCheckout()"
              class="bg-[#fd374f] w-full text-white text-[21px] font-semibold p-1.5 rounded-full mt-4"
            >
              Checkout
            </button>
          </div>

          <div class="bg-white p-4 mt-4 rounded-lg">
            <div class="text-lg font-semibold mb-2">Payment methods</div>
            <div
              class="flex items-center md:justify-between justify-start gap-8 my-4"
            >
              <div v-for="card of cards">
                <img
                  class="h-6"
                  :src="card"
                  :title="card.split('.')[0]"
                  alt="card"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </MainLayout>
</template>

<script setup>
import MainLayout from '@/layouts/MainLayout.vue'
import { useUserStore } from '@/stores/user'
const userStore = useUserStore()

let selectedArray = ref([])

const cards = ref(['visa.png', 'mastercard.png', 'paypal.png', 'applepay.png'])

const products = [
  {
    id: 1,
    title:
      'Lorem ipsum dolor sit, amet consectetur adipisicing elit. Officiis deserunt cumque iusto dolor a autem. Obcaecati, facilis ratione in blanditiis nam odit velit, sunt animi quam fugiat ipsam consequatur nisi?',
    description: 'This is a description',
    url: 'https://picsum.photos/id/12/800/800',
    price: 12000
  },
  {
    id: 2,
    title: 'Title 2',
    description: 'This is a description',
    url: 'https://picsum.photos/id/21/800/800',
    price: 2000
  },
  {
    id: 3,
    title: 'Title 3',
    description: 'This is a description',
    url: 'https://picsum.photos/id/214/800/800',
    price: 3500
  }
]

onMounted(() => {
  setTimeout(() => (userStore.isLoading = false), 200)
})

const totalPriceComputed = computed(() => {
  if (userStore.cart.length) {
    const total = userStore.cart
      .map((prod) => prod.price)
      .reduce((acc, cur) => acc + cur)
    return total / 100
  }
  return 0
})

const selectedRadioFunc = (val) => {
  if (!selectedArray.value.length) {
    selectedArray.value.push(val)
    return
  }

  selectedArray.value.forEach((item, index) => {
    if (val.id !== item.id) {
      selectedArray.value.push(val)
    } else {
      selectedArray.value.splice(index, 1)
    }
  })

  console.log(selectedArray.value)
}

const goToCheckout = () => {
  alert('checkout')
}
</script>
