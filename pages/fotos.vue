<template>
    <div class="min-h-screen bg-gradient-to-b from-gray-900 to-gray-800 pt-24 pb-12">
        <!-- Hero Carousel Section -->
        <div class="max-w-7xl mx-auto px-4 mb-16">
            <h1 class="text-4xl md:text-5xl font-bold text-white mb-8 text-center">Foto's</h1>

            <!-- Carousel -->
            <div class="relative group">
                <!-- Main Carousel Image -->
                <div class="relative h-[70vh] overflow-hidden rounded-2xl">
                    <img :src="images[currentImageIndex].url" :alt="images[currentImageIndex].title"
                        class="w-full h-full object-cover transition-transform duration-700" />

                    <!-- Image Overlay with Title -->
                    <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black/70 to-transparent p-8">
                        <h2 class="text-2xl text-white font-semibold mb-2">
                            {{ images[currentImageIndex].title }}
                        </h2>
                        <p class="text-gray-300">
                            {{ images[currentImageIndex].description }}
                        </p>
                    </div>

                    <!-- Navigation Arrows -->
                    <button @click="previousImage"
                        class="absolute left-4 top-1/2 -translate-y-1/2 bg-black/50 hover:bg-black/70 text-white p-2 rounded-full backdrop-blur-sm opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                        aria-label="Previous image">
                        <ChevronLeft class="w-6 h-6" />
                    </button>

                    <button @click="nextImage"
                        class="absolute right-4 top-1/2 -translate-y-1/2 bg-black/50 hover:bg-black/70 text-white p-2 rounded-full backdrop-blur-sm opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                        aria-label="Next image">
                        <ChevronRight class="w-6 h-6" />
                    </button>
                </div>

                <!-- Thumbnails -->
                <div class="mt-4 flex justify-center space-x-2 overflow-x-auto pb-2">
                    <button v-for="(image, index) in images" :key="index" @click="currentImageIndex = index"
                        class="relative flex-shrink-0 h-20 w-20 rounded-lg overflow-hidden transition-transform duration-300 hover:scale-105"
                        :class="{ 'ring-2 ring-emerald-500': currentImageIndex === index }">
                        <img :src="image.url" :alt="image.title" class="w-full h-full object-cover" />
                        <div class="absolute inset-0 bg-black/30"
                            :class="{ 'bg-transparent': currentImageIndex === index }"></div>
                    </button>
                </div>
            </div>
        </div>

        <!-- Photo Grid Section -->
        <div class="max-w-7xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-white mb-8">Alle Foto's</h2>

            <!-- Filter Buttons -->
            <div class="flex flex-wrap gap-4 mb-8">
                <button v-for="category in categories" :key="category" @click="selectedCategory = category"
                    class="px-4 py-2 rounded-full text-sm transition-colors duration-300" :class="[
                        selectedCategory === category
                            ? 'bg-emerald-500 text-white'
                            : 'bg-gray-800 text-gray-300 hover:bg-gray-700'
                    ]">
                    {{ category }}
                </button>
            </div>

            <!-- Photo Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div v-for="(image, index) in filteredImages" :key="index"
                    class="group relative aspect-square rounded-xl overflow-hidden cursor-pointer"
                    @click="openLightbox(index)">
                    <img :src="image.url" :alt="image.title"
                        class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110" />

                    <!-- Hover Overlay -->
                    <div
                        class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                        <div class="absolute bottom-0 left-0 right-0 p-6">
                            <h3 class="text-white font-semibold text-lg mb-2">{{ image.title }}</h3>
                            <p class="text-gray-300 text-sm">{{ image.description }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Lightbox -->
        <div v-if="lightboxOpen" class="fixed inset-0 bg-black/90 z-50 flex items-center justify-center"
            @click="closeLightbox">
            <div class="relative max-w-7xl mx-auto px-4">
                <img :src="images[lightboxIndex].url" :alt="images[lightboxIndex].title"
                    class="max-h-[90vh] max-w-full object-contain" />

                <button @click="closeLightbox"
                    class="absolute top-4 right-4 text-white hover:text-gray-300 transition-colors duration-300">
                    <X class="w-8 h-8" />
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { ChevronLeft, ChevronRight, X } from 'lucide-vue-next'

// Sample data - replace with your actual images
const images = ref([
    {
        url: 'risotto.jpeg',
        title: 'Favourite Food',
        description: 'Mijn favoriet soort eten.',
        category: 'Food'
    },
    {
        url: 'rocky.jpeg',
        title: 'Favourite Movie',
        description: 'Mijn favoriete film over een boxer.',
        category: 'Hobbies'
    },
    {
        url: 'bbking.jpeg',
        title: 'Favourite Artist',
        description: 'Een man die de genre van blues speelde.',
        category: 'Hobbies'
    },
    {
        url: 'images-2.jpeg',
        title: 'Favourite Burger',
        description: 'Beste burgers and fries',
        category: 'Food'
    },
    {
        url: 'cadillac.jpg',
        title: 'Favourite Car',
        description: 'Mijn favoriete auto.',
        category: 'Hobbies'
    },
    {
        url: 'itallainfood.jpg',
        title: 'Favourite Burger',
        description: 'Beste burgers and fries',
        category: 'Food'
    },
    {
        url: 'Roger-Federer-Olympics-scaled.jpg',
        title: 'Favourite Athlete',
        description: 'Beste burgers and fries',
        category: 'Sport'
    },
    {
        url: 'rugby.webp',
        title: 'Favourite Sport',
        description: 'Beste burgers and fries',
        category: 'Sport'
    },
    // Add more images as needed...
])

const categories = ['All', 'Hobbies', 'Food', 'Sport']
const selectedCategory = ref('All')
const currentImageIndex = ref(0)
const lightboxOpen = ref(false)
const lightboxIndex = ref(0)

// Filter images based on selected category
const filteredImages = computed(() => {
    if (selectedCategory.value === 'All') return images.value
    return images.value.filter(image => image.category === selectedCategory.value)
})

// Carousel navigation
const nextImage = () => {
    currentImageIndex.value = (currentImageIndex.value + 1) % images.value.length
}

const previousImage = () => {
    currentImageIndex.value = currentImageIndex.value === 0
        ? images.value.length - 1
        : currentImageIndex.value - 1
}

// Auto advance carousel (optional)
onMounted(() => {
    const interval = setInterval(nextImage, 5000)
    onUnmounted(() => clearInterval(interval))
})

// Lightbox functions
const openLightbox = (index) => {
    lightboxIndex.value = index
    lightboxOpen.value = true
    document.body.style.overflow = 'hidden'
}

const closeLightbox = () => {
    lightboxOpen.value = false
    document.body.style.overflow = ''
}

// Keyboard navigation
onMounted(() => {
    const handleKeydown = (e) => {
        if (!lightboxOpen.value) return

        switch (e.key) {
            case 'ArrowLeft':
                previousImage()
                break
            case 'ArrowRight':
                nextImage()
                break
            case 'Escape':
                closeLightbox()
                break
        }
    }

    window.addEventListener('keydown', handleKeydown)
    onUnmounted(() => window.removeEventListener('keydown', handleKeydown))
})
</script>