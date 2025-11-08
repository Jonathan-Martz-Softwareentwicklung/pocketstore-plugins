<template>
  <div class="min-h-screen bg-base-100 text-base-content">

   <section class="pt-6 px-3">
     <label class="floating-label">
       <span>Wonach suchst du ?</span>
       <input type="text" class="input w-full" />
     </label>
   </section>
    
    <!-- Featured Categories -->
    <section class="py-8 bg-base-200">
      <div class="container mx-auto px-4 text-center">
        <h2 class="text-3xl font-bold mb-8">Popular Categories</h2>
        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-6">
          <div v-for="cat in categories" :key="cat.title"
               class="card bg-base-100 shadow-md hover:shadow-xl transition">
            <figure><img :src="cat.image" :alt="cat.title"/></figure>
            <div class="card-body p-4">
              <h3 class="text-lg font-semibold">{{ cat.title }}</h3>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Product Grid -->
    <section class="py-16">
      <div class="container mx-auto px-4">
        <h2 class="text-3xl font-bold text-center mb-8">Trending Products</h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
          <div v-for="p in products" :key="p.title"
               class="card bg-base-100 shadow-md hover:shadow-xl transition">
            <figure><img :src="p.image" :alt="p.title"/></figure>
            <div class="card-body">
              <h3 class="card-title">{{ p.title }}</h3>
              <p class="text-sm text-gray-500">{{ p.category }}</p>
              <div class="card-actions justify-between items-center mt-4">
                <span class="font-bold text-lg">{{ p.price }}</span>
                <button class="btn btn-sm btn-primary">View</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials -->
    <section class="py-16 bg-base-200">
      <div class="container mx-auto px-4 text-center">
        <h2 class="text-3xl font-bold mb-8">What Our Users Say</h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div v-for="t in testimonials" :key="t.name"
               class="card bg-base-100 shadow-md p-6">
            <p class="italic mb-4">“{{ t.quote }}”</p>
            <div class="flex items-center justify-center gap-3">
              <div class="avatar">
                <div class="w-12 rounded-full">
                  <img :src="t.avatar"/>
                </div>
              </div>
              <div class="text-left">
                <p class="font-semibold">{{ t.name }}</p>
                <p class="text-sm text-gray-500">{{ t.role }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
const categories = [
  {title: "Art", image: "https://source.unsplash.com/400x300/?art"},
  {title: "Tech", image: "https://source.unsplash.com/400x300/?technology"},
  {title: "Fashion", image: "https://source.unsplash.com/400x300/?fashion"},
  {title: "Home", image: "https://source.unsplash.com/400x300/?home"},
  {title: "Home", image: "https://source.unsplash.com/400x300/?home"},
  {title: "Home", image: "https://source.unsplash.com/400x300/?home"},
]

const products = [
  {title: "Handcrafted Mug", price: "$24", category: "Home", image: "https://source.unsplash.com/400x300/?mug"},
  {
    title: "Wireless Headphones",
    price: "$99",
    category: "Tech",
    image: "https://source.unsplash.com/400x300/?headphones"
  },
  {title: "Vintage Jacket", price: "$65", category: "Fashion", image: "https://source.unsplash.com/400x300/?jacket"},
  {title: "Abstract Painting", price: "$120", category: "Art", image: "https://source.unsplash.com/400x300/?painting"},
]

const testimonials = [
  {
    name: "Sarah Johnson",
    role: "Artist",
    quote: "MarketMate helped me reach new customers around the world!",
    avatar: "https://i.pravatar.cc/100?img=12",
  },
  {
    name: "James Lee",
    role: "Tech Seller",
    quote: "The best marketplace platform I’ve ever used.",
    avatar: "https://i.pravatar.cc/100?img=5",
  },
  {
    name: "Maria Gomez",
    role: "Designer",
    quote: "Beautiful interface and excellent support!",
    avatar: "https://i.pravatar.cc/100?img=47",
  },
]
</script>

<style scoped>
.container {
  max-width: 1200px;
}
</style>
