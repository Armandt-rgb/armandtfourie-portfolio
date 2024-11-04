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
                    <button @click="isOpen = !isOpen"
                        class="md:hidden text-gray-300 hover:text-white focus:outline-none">
                        <div class="relative w-6 h-6">
                            <span :class="[
                                'absolute h-0.5 w-6 bg-current transform transition-all duration-300',
                                isOpen ? 'rotate-45 translate-y-0' : '-translate-y-2'
                            ]"></span>
                            <span :class="[
                                'absolute h-0.5 w-6 bg-current transform transition-all duration-300',
                                isOpen ? 'opacity-0' : 'opacity-100'
                            ]"></span>
                            <span :class="[
                                'absolute h-0.5 w-6 bg-current transform transition-all duration-300',
                                isOpen ? '-rotate-45 translate-y-0' : 'translate-y-2'
                            ]"></span>
                        </div>
                    </button>
                </div>
            </div>

            <!-- Mobile Navigation -->
            <div :class="[
                'md:hidden transition-all duration-300 ease-in-out overflow-hidden',
                isOpen ? 'max-h-96 opacity-100' : 'max-h-0 opacity-0'
            ]">
                <div class="px-4 pt-2 pb-6 space-y-2 bg-gray-900/95 backdrop-blur-md">
                    <NuxtLink v-for="item in menuItems" :key="item.path" :to="item.path" @click="isOpen = false"
                        class="block py-3 px-4 text-gray-300 hover:text-white hover:bg-gray-800/50 rounded-lg transition-colors duration-300 text-sm uppercase tracking-wider">
                        {{ item.name }}
                    </NuxtLink>
                </div>
            </div>
        </nav>
        <slot />
        
    </div>
</template>
<script setup>
const menuItems = [
    { name: 'HOME', path: '/' },
    { name: 'WIE BEN IK?', path: '/wie-ben-ik' },
    { name: 'WAT KAN IK?', path: '/wat-kan-ik' },
    { name: 'WAT WIL IK?', path: '/wat-wil-ik' }
]
</script>