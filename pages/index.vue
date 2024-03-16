<template>
  <MainLayout>
    <section id="IndexPage" class="mt-4 max-2-[1200px] mx-auto px-2">
      <div
        class="grid xl:grid-cols-6 lg:grid-cols-5 md:grid-cols-4 sm:grid-cols-2"
      >
        <div v-if="products" v-for="product in products" :key="product.id">
          <Products :product="product" />
        </div>
      </div>
    </section>
  </MainLayout>
</template>

<script setup>
import MainLayout from '@/layouts/MainLayout.vue'

const products = [
  {
    id: 1,
    title:
      'Lorem ipsum dolor sit, amet consectetur adipisicing elit. Officiis deserunt cumque iusto dolor a autem. Obcaecati, facilis ratione in blanditiis nam odit velit, sunt animi quam fugiat ipsam consequatur nisi?',
    description: 'This is a description',
    url: 'https://picsum.photos/id/12/800/800',
    price: 9999
  },
  {
    id: 2,
    title: 'Title 2',
    description: 'This is a description',
    url: 'https://picsum.photos/id/21/800/800',
    price: 9999
  },
  {
    id: 3,
    title:
      'erunt cumque iusto dolor a autem. Obcaecati, facilis ration, erunt cumque iusto dolor a autem. Obcaecati, facilis ration',
    description: 'This is a description',
    url: 'https://picsum.photos/id/32/800/800',
    price: 9999
  },
  {
    id: 4,
    title:
      'erunt cumque iusto dolor a autem. Obcaecati, facilis ration, erunt cumque iusto dolor a autem. Obcaecati, facilis ration',
    description: 'This is a description',
    url: 'https://picsum.photos/id/412/800/800',
    price: 9999
  },
  {
    id: 5,
    title: 'Title 5',
    description: 'This is a description',
    url: 'https://picsum.photos/id/51/800/800',
    price: 9999
  },
  {
    id: 6,
    title:
      'erunt cumque iusto dolor a autem. Obcaecati, facilis ration, erunt cumque iusto dolor a autem. Obcaecati, facilis ration',
    description: 'This is a description',
    url: 'https://picsum.photos/id/61/800/800',
    price: 9999
  },
  {
    id: 7,
    title:
      'erunt cumque iusto dolor a autem. Obcaecati, facilis ration, erunt cumque iusto dolor a autem. Obcaecati, facilis ration',
    description: 'This is a description',
    url: 'https://picsum.photos/id/17/800/800',
    price: 9999
  },
  {
    id: 8,
    title: 'Title 8',
    description: 'This is a description',
    url: 'https://picsum.photos/id/81/800/800',
    price: 9999
  },
  {
    id: 9,
    title: 'Title 9',
    description: 'This is a description',
    url: 'https://picsum.photos/id/91/800/800',
    price: 9999
  },
  {
    id: 10,
    title: 'Title 10',
    description: 'This is a description',
    url: 'https://picsum.photos/id/10/800/800',
    price: 9999
  }
]
</script>
