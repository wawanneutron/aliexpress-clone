<template>
  <MainLayout>
    <div id="ItemPage" class="mt-4 max-w-[1200px] mx-auto px-2">
      <div class="md:flex gap-4 justify-between mx-auto w-full">
        <div class="md:w-[40%]">
          <img
            class="rounded-lg object-fit"
            :src="currentImage"
            alt="detail-mage"
          />

          <div
            v-if="images[0] !== ''"
            class="flex items-center justify-center mt-2"
          >
            <div v-for="image in images">
              <img
                @mouseover="currentImage = image"
                @click="currentImage = image"
                width="70"
                class="rounded-md object-fit border-[3px] cursor-pointer"
                :class="currentImage === image ? 'border-[#ff5353]' : ''"
                :src="image"
                alt="thumbnail-img"
              />
            </div>
          </div>
        </div>

        <div class="md:w-[60%] bg-white p-3 rounded-lg">
          <div>
            <p class="mb-2">Title</p>
            <p class="font-light text-[12px] mb-2">Description Section</p>
          </div>

          <div class="flex items-center pt-1.5">
            <span class="h-4 min-w-4 rounded-full p-0.5 bg-[#ffd000] mr-2">
              <Icon name="mdi:star" class="-mt-[17px]" size="12" />
            </span>
            <p class="text-[#ff5353]">Extra 5% off</p>
          </div>

          <div class="flex items-center justify-start my-2">
            <Icon name="mdi:star" color="#ff5353" />
            <Icon name="mdi:star" color="#ff5353" />
            <Icon name="mdi:star" color="#ff5353" />
            <Icon name="mdi:star" color="#ff5353" />
            <Icon name="mdi:star" color="#ff5353" />
            <span class="text-[13px] font-light ml-2"
              >5 212 Reviews 1,000+ orders</span
            >
          </div>

          <div class="border-b" />

          <div class="flex items-center justify-start gap-2 my-2">
            <div class="text-xl font-bold">Rp {{ priceComputed }}</div>
            <span
              class="bg-[#f5f5f5] border text-[#c08562] text-[9px] font-semibold px-1.5 rounded-sm"
              >70% off</span
            >
          </div>

          <p class="text-[#009a66] text-xs font-semibold pt-1">
            Free 11-day delivery over Rp 12.000
          </p>
          <p class="text-[#009a66] text-xs font-semibold pt-1">Free Shipping</p>

          <div class="py-2"></div>

          <button
            @click="addToCart()"
            :disabled="isInCart"
            class="px-6 py-2 rounded-lg text-white text-lg font-semibold bg-gradient-to-r from-[#ff851a] to-[#ffac2c]"
          >
            <div v-if="isInCart">Is Added</div>
            <div v-else>Add to Cart</div>
          </button>
        </div>
      </div>
    </div>
  </MainLayout>
</template>

<script setup>
import MainLayout from '@/layouts/MainLayout.vue'
import { useUserStore } from '@/stores/user'

const userStore = useUserStore()
const route = useRoute()

let currentImage = ref(null)

onMounted(() => {
  watchEffect(() => {
    images.value[0] = 'https://picsum.photos/id/77/800/800'
    currentImage.value = 'https://picsum.photos/id/77/800/800'
  })
})

const isInCart = computed(() => {
  let res = false

  userStore.cart.forEach((prod) => {
    if (route.params.id == prod.id) {
      res = true
    }
  })
  return res
})

const priceComputed = computed(() => '175.000')

const images = ref([
  '',
  'https://picsum.photos/id/212/800/800',
  'https://picsum.photos/id/215/800/800',
  'https://picsum.photos/id/312/800/800',
  'https://picsum.photos/id/232/800/800',
  'https://picsum.photos/id/142/800/800'
])

const addToCart = () => {
  alert('Added')
}
</script>
