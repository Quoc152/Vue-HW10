<script setup>
import { ref } from 'vue';
import { Sparkles, Truck, AlertTriangle } from 'lucide-vue-next';

const products = ref([
  {
    id: 1,
    name: "Smartphone X",
    image: "/placeholder.svg?height=300&width=400",
    description: "Latest model with advanced features.",
    originalPrice: 20,
    salePrice: 10,
    badges: ["New", "Free Shipping"]
  },
  {
    id: 2,
    name: "Laptop Pro",
    image: "/placeholder.svg?height=300&width=400",
    description: "High-performance laptop for professionals.",
    originalPrice: 30,
    salePrice: 20,
    badges: ["Limited Stock"]
  },
  {
    id: 3,
    name: "Wireless Earbuds",
    image: "/placeholder.svg?height=300&width=400",
    description: "Crystal clear sound with long battery life.",
    originalPrice: 40,
    salePrice: 20,
    badges: ["New", "Free Shipping", "Limited Stock"]
  }
]);

const formatPrice = (price) => {
  return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(price);
};

const getBadgeIcon = (badge) => {
  switch (badge) {
    case 'New':
      return Sparkles;
    case 'Free Shipping':
      return Truck;
    case 'Limited Stock':
      return AlertTriangle;
    default:
      return null;
  }
};
</script>

<template>
  <div class="container mx-auto p-4">
    <h1 class="text-3xl font-bold mb-6">Product List</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <div v-for="product in products" :key="product.id" class="bg-white rounded-lg shadow-md overflow-hidden">
        <img :src="product.image" :alt="product.name" class="w-full h-48 object-cover">
        <div class="p-4">
          <h2 class="text-black text-xl font-semibold mb-2">{{ product.name }}</h2>
          <p class="text-gray-600 mb-4">{{ product.description }}</p>
          <div class="flex justify-between items-center mb-4">
            <div>
              <span class="text-gray-500 line-through mr-2">{{ formatPrice(product.originalPrice) }}</span>
              <span class="text-xl font-bold text-red-600">{{ formatPrice(product.salePrice) }}</span>
            </div>
            <button class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700 transition duration-300">
              Add to Cart
            </button>
          </div>
          <div class="flex flex-wrap gap-2">
            <span v-for="badge in product.badges" :key="badge" 
                  class="px-2 py-1 text-xs font-semibold rounded flex items-center"
                  :class="{
                    'bg-green-100 text-green-800': badge === 'New',
                    'bg-blue-100 text-blue-800': badge === 'Free Shipping',
                    'bg-yellow-100 text-yellow-800': badge === 'Limited Stock'
                  }">
              <component :is="getBadgeIcon(badge)" class="w-4 h-4 mr-1" />
              {{ badge }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
