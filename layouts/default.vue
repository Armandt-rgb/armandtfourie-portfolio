<template>
    <div class="min-h-screen">
        <nav :class="[
            'fixed top-0 left-0 w-full z-50 transition-all duration-300',
            scrolled ? 'bg-gray-900/95 backdrop-blur-md shadow-lg' : 'bg-transparent'
        ]">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex items-center justify-between h-20">
                    <!-- Logo -->
                    <NuxtLink to="/" class="flex items-center space-x-2 group">
                        <img src="/images/logo.png" alt="Logo"
                            class="w-12 h-12 rounded-full transition-transform group-hover:scale-110" />
                        <span class="text-white text-xl font-semibold hidden sm:block">Armandt Fourie Portfolio

                        </span>
                    </NuxtLink>

                    <!-- Desktop Navigation -->
                    <div class="hidden md:flex items-center space-x-8">
                        <NuxtLink v-for="item in menuItems" :key="item.path" :to="item.path"
                            class="text-gray-300 hover:text-white transition-colors duration-300 relative group text-sm uppercase tracking-wider">
                            {{ item.name }}
                            <span
                                class="absolute bottom-0 left-0 w-full h-0.5 bg-white transform scale-x-0 group-hover:scale-x-100 transition-transform duration-300"></span>
                        </NuxtLink>
                    </div>

                    <!-- Mobile menu button -->
                    <button @click="toggleMenu" class="md:hidden text-gray-300 hover:text-white focus:outline-none p-2"
                        aria-label="Toggle menu">
                        <div class="relative w-6 h-5">
                            <span :class="[
                                'absolute h-0.5 w-6 bg-current transform transition-all duration-300',
                                isOpen ? 'rotate-45 translate-y-2.5' : ''
                            ]"></span>
                            <span :class="[
                                'absolute h-0.5 w-6 bg-current transform transition-all duration-300 top-2',
                                isOpen ? 'opacity-0' : 'opacity-100'
                            ]"></span>
                            <span :class="[
                                'absolute h-0.5 w-6 bg-current transform transition-all duration-300 top-4',
                                isOpen ? '-rotate-45 -translate-y-2.5' : ''
                            ]"></span>
                        </div>
                    </button>
                </div>
            </div>

            <Transition enter-active-class="transition duration-200 ease-out" enter-from-class="translate-y-1 opacity-0"
                enter-to-class="translate-y-0 opacity-100" leave-active-class="transition duration-150 ease-in"
                leave-from-class="translate-y-0 opacity-100" leave-to-class="translate-y-1 opacity-0">
                <div v-show="isOpen"
                    class="md:hidden absolute top-full left-0 w-full bg-gray-900/95 backdrop-blur-md shadow-lg py-2">
                    <div class="px-4 pt-2 pb-3 space-y-1">
                        <NuxtLink v-for="item in menuItems" :key="item.path" :to="item.path"
                            class="block px-4 py-3 text-gray-300 hover:text-white hover:bg-gray-800/50 rounded-lg transition-colors duration-300 text-sm uppercase tracking-wider"
                            @click="closeMenu">
                            {{ item.name }}
                        </NuxtLink>
                    </div>
                </div>
            </Transition>

        </nav>
        <slot />

    </div>
</template>
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import {
    Github,
    Linkedin,
    Twitter,
    Instagram
} from 'lucide-vue-next'

const isOpen = ref(false)
const scrolled = ref(false)

const menuItems = [
    { name: 'HOME', path: '/' },
    { name: 'WIE BEN IK?', path: '/wie-ben-ik' },
    { name: 'WAT KAN IK?', path: '/wat-kan-ik' },
    { name: 'WAT WIL IK?', path: '/wat-wil-ik' },
    { name: 'FOTO\'S', path: '/fotos' }
]

const socialLinks = [
    { name: 'GitHub', url: '#', icon: Github },
    { name: 'LinkedIn', url: '#', icon: Linkedin },
    { name: 'Twitter', url: '#', icon: Twitter },
    { name: 'Instagram', url: '#', icon: Instagram }
]

const toggleMenu = () => {
    isOpen.value = !isOpen.value
    if (isOpen.value) {
        document.body.style.overflow = 'hidden'
    } else {
        document.body.style.overflow = ''
    }
}

const closeMenu = () => {
    isOpen.value = false
    document.body.style.overflow = ''
}

const handleScroll = () => {
    scrolled.value = window.scrollY > 20
}

const handleResize = () => {
    if (window.innerWidth >= 768 && isOpen.value) {
        closeMenu()
    }
}

onMounted(() => {
    window.addEventListener('scroll', handleScroll)
    window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll)
    window.removeEventListener('resize', handleResize)
})
</script>