<template>
    <div class="hero relative h-screen w-full flex items-center justify-center">
        <video autoplay loop muted playsinline class="absolute inset-0 w-full h-full object-cover -z-10">
            <source src="/videos/fighter-jet.mp4" type="video/mp4" />
        </video>
        <div class="absolute inset-0 bg-[rgba(12,3,51,0.3)]"></div>

        <div class="content text-center z-10">
            <h1
                class="text-8xl text-white font-semibold transition duration-500 hover:text-transparent hover:bg-clip-text hover:bg-gradient-to-r from-white to-white">
                Jouw gids naar Armandt
            </h1>
            <NuxtLink to="/fotos"
                class="inline-block mt-5 px-14 py-4 text-2xl text-white border-2 border-white rounded-full hover:text-transparent hover:bg-clip-text hover:bg-gradient-to-r from-white to-white transition duration-500">
                Foto's
            </NuxtLink>
        </div>
    </div>
</template>