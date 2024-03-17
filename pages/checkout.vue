<template>
  <MainLayout>
    <section id="CheckoutPage" class="mt-4 max-w-[1200px] mx-auto px-2">
      <div class="md:flex gap-4 justify-between mx-auto w-full">
        <div class="md:w-[65%]">
          <div class="bg-white rounded-lg p-4">
            <div class="text-xl font-semibold mb-2">Shipping Address</div>

            <div v-if="true">
              <NuxtLink
                to="/address"
                class="flex items-center pb-2 text-blue-500 hover:text-red-400"
              >
                <Icon name="ic:round-plus" size="18" class="mr-2" />
                Update Address
              </NuxtLink>

              <div class="pt-2 border-t">
                <div class="underline pb-1">Delivery Address</div>

                <ul class="text-xs">
                  <li class="flex items-center gap-2">
                    <div>Contact Name:</div>
                    <div class="font-bold">TEST</div>
                  </li>
                  <li class="flex items-center gap-2">
                    <div>Address:</div>
                    <div class="font-bold">TEST</div>
                  </li>
                  <li class="flex items-center gap-2">
                    <div>ZIp Code:</div>
                    <div class="font-bold">TEST</div>
                  </li>
                  <li class="flex items-center gap-2">
                    <div>City:</div>
                    <div class="font-bold">TEST</div>
                  </li>
                  <li class="flex items-center gap-2">
                    <div>Country:</div>
                    <div class="font-bold">TEST</div>
                  </li>
                </ul>
              </div>
            </div>

            <NuxtLink
              v-else
              to="/address"
              class="flex items-center text-blue-500 hover:text-red-400"
            >
              <Icon name="ic:round-add" size="18" class="mr-2" />
              Add New Address
            </NuxtLink>
          </div>

          <div class="bg-white rounded-lg p-4 mt-4">
            <div v-for="product in products">
              <CheckoutItem :product="product" />
            </div>
          </div>
        </div>

        <div class="md:hidden block my-4" />

        <div class="md:w-[35%]">
          <div class="bg-white rounded-lg p-4">
            <div class="text-2xl font-extrabold mb-2">Summary</div>

            <div class="flex items-center justify-between my-4">
              <div>Total Shipping</div>
              <div>Free</div>
            </div>

            <div class="border-t" />

            <div class="flex items-center justify-between my-4">
              <div class="font-semibold">Total</div>
              <div class="font-semibold text-2xl">
                $ <span class="font-extrabold">{{ total / 100 }}</span>
              </div>
            </div>

            <form @submit.prevent="pay()">
              <div class="border border-gray-500 p-2 rounded-sm" />
              <p role="alert" class="text-red-700 text-center font-semibold" />

              <button
                :disabled="isProcessing"
                type="submit"
                class="mt-4 bg-gradient-to-r from-[#fe630c] to-[#ff3200] w-full text-white text-[21px] font-semibold p-1.5 rounded-full"
              >
                <Icon v-if="isProcessing" name="eos-icons:loading" size="28" />
                <div v-else>Place order</div>
              </button>
            </form>
          </div>

          <div class="bg-white rounded-lg p-4 mt-4">
            <div class="text-lg font-semibold mb-2 mt-2">AliExpress</div>
            <div class="my-2">
              AliExpress keeps your information and payment safe
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

let isProcessing = ref(false)

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
}

const goToCheckout = () => {
  let ids = []
  userStore.checkout = []

  selectedArray.value.forEach((item) => ids.push(item.id))

  let res = userStore.cart.filter((item) => {
    return ids.indexOf(item.id) !== -1
  })

  res.forEach((item) => userStore.checkout.push(toRaw(item)))

  return navigateTo('/checkout')
}

const pay = () => {
  //
}
</script>
