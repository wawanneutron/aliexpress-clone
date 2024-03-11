<template>
  <div
    class="bg-white m-1.5 inline-block rounded hover:shadow-[0_0_10px_3px_rgba(0,0,0,0.15)] cusrsor-pointer"
  >
    <NuxtLink :to="`/item/${product.id}`">
      <img :src="product.url" :alt="product.title" />

      <div id="ProductDetail" class="flex flex-col justify-between h-[140px]">
        <span class="flex items-center justify-start gap-3 px-1 pt-1">
          <span class="text-[#ff6674] font-semibold">${{ priceComputed }}</span>
          <span class="text-gray-500 text-sm text-light line-through"
            >${{ oldPriceComputed }}</span
          >
        </span>

        <span
          class="px-1 relative -top-1.5 text-[#ff6674] text-xs font-semibold"
        >
          Extra 5% off
        </span>

        <div class="flex items-center gap-1 px-1 relative -top-1">
          <span
            class="bg-[#fd374f] text-white text-[9px] font-semibold px-1.5 rounded-sm"
            >Welcome Deal</span
          >
          <span
            class="bg-[#f5f5f5] border text-[#c08562] text-[9px] font-semibold px-1.5 rounded-sm"
            >Top Selling</span
          >
        </div>

        <p class="flex items-center px-1 text-xs text-[#252525]">
          5,000+ sold
          <Icon name="mdi:star" color="#757575" class="ml-1.5" />
          4.7
        </p>

        <p class="px-1 pt-0.5 text-xs text-[#252525] two-lines">
          {{ product.title }}
        </p>

        <p class="px-1 pb-1">
          <span class="text-[#009A66] text-xs font-semibold"
            >Free Shipping</span
          >
        </p>
      </div>
    </NuxtLink>
  </div>
</template>

<script setup>
const props = defineProps(['product'])
const { product } = toRefs(props)

const priceComputed = computed(() => {
  return product.value.price / 100
})

const oldPriceComputed = computed(() => {
  const price = (product.value.price + product.value.price / 20) / 100

  return price.toFixed(2)
})
</script>

<style>
.two-lines {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2; /* number of lines to show */
  -webkit-box-orient: vertical;
}
</style>
