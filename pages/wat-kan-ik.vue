<template>
    <div class="min-h-screen bg-gradient-to-b from-gray-900 to-gray-800 pt-24 px-4 pb-12">
        <div class="max-w-7xl mx-auto">
            <!-- Hero Section -->
            <div class="text-center mb-16">
                <h1 class="text-4xl md:text-5xl font-bold text-white mb-4">
                    Wat kan ik?
                </h1>
                <p class="text-gray-400 text-lg max-w-2xl mx-auto">
                    Een overzicht van mijn vaardigheden, expertise en technische kennis die ik heb opgebouwd door de
                    jaren heen.
                </p>
            </div>

            <!-- Main Skills Section -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 mb-16">
                <div v-for="(category, index) in skillCategories" :key="index"
                    class="bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 transform hover:-translate-y-2 transition-all duration-300 hover:shadow-xl hover:shadow-purple-500/10">
                    <div class="flex items-center mb-4">
                        <component :is="category.icon" class="w-8 h-8 text-purple-500 mr-3" />
                        <h2 class="text-xl font-semibold text-white">{{ category.title }}</h2>
                    </div>
                    <div class="space-y-4">
                        <div v-for="skill in category.skills" :key="skill.name" class="group">
                            <div class="flex justify-between items-center mb-1">
                                <span class="text-gray-300 group-hover:text-white transition-colors duration-300">
                                    {{ skill.name }}
                                </span>
                                <span class="text-gray-400 text-sm">{{ skill.level }}%</span>
                            </div>
                            <div class="h-2 bg-gray-700 rounded-full overflow-hidden">
                                <div class="h-full bg-gradient-to-r from-purple-500 to-purple-700 rounded-full transition-all duration-1000 ease-out"
                                    :style="{ width: `${skill.level}%` }"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Projects Section
            <h2 class="text-3xl font-bold text-white mb-8 text-center">Projecten & Ervaring</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-16">
                <div v-for="project in projects" :key="project.title"
                    class="bg-gray-800/50 backdrop-blur-sm rounded-xl overflow-hidden group hover:shadow-xl hover:shadow-purple-500/10 transition-all duration-300">
                    <div class="relative h-48 overflow-hidden">
                        <img :src="project.image" :alt="project.title"
                            class="w-full h-full object-cover transform group-hover:scale-110 transition-transform duration-500" />
                        <div class="absolute inset-0 bg-gradient-to-t from-gray-900 to-transparent opacity-60"></div>
                    </div>
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-white mb-2">{{ project.title }}</h3>
                        <p class="text-gray-400 mb-4">{{ project.description }}</p>
                        <div class="flex flex-wrap gap-2">
                            <span v-for="tech in project.technologies" :key="tech"
                                class="px-3 py-1 text-sm text-purple-300 bg-purple-500/10 rounded-full">
                                {{ tech }}
                            </span>
                        </div>
                    </div>
                </div>
            </div> -->

            <!-- Education & Certifications -->
            <h2 class="text-3xl font-bold text-white mb-8 text-center">Opleiding & Certificeringen</h2>
            <div class="space-y-6 max-w-3xl mx-auto">
                <div v-for="edu in education" :key="edu.title"
                    class="bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 transform hover:-translate-x-2 transition-all duration-300">
                    <div class="flex items-start justify-between">
                        <div>
                            <h3 class="text-xl font-semibold text-white mb-1">{{ edu.title }}</h3>
                            <p class="text-purple-400">{{ edu.institution }}</p>
                            <p class="text-gray-400 mt-2">{{ edu.description }}</p>
                        </div>
                        <span class="text-gray-400 text-sm">{{ edu.year }}</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import {
    Code2,
    Paintbrush,
    Brain,
    Database,
    Laptop,
    Settings
} from 'lucide-vue-next'

const skillCategories = [
    {
        title: 'School',
        icon: Code2,
        skills: [
            { name: 'Geschiedenis', level: 90 },
            { name: 'Engels', level: 85 },
            { name: 'Afrikaans', level: 80 },
            
        ]
    },
    {
        title: 'Sporten',
        icon: Paintbrush,
        skills: [
            { name: 'Tennis', level: 85 },
            { name: 'Rugby', level: 80 },
            { name: 'Boogschieten', level: 75 },
            { name: 'Hockey', level: 70 }
        ]
    },
    {
        title: 'Hobbys',
        icon: Database,
        skills: [
            { name: 'Tennis', level: 75 },
            { name: 'Gitaar', level: 70 },
            { name: 'Piano', level: 65 },
            { name: 'Rugby', level: 60 }
        ]
    },
    {
        title: 'Eten',
        icon: Brain,
        skills: [
            { name: 'Burgers', level: 95 },
            { name: 'Pasta', level: 90 },
            { name: 'Lasagna', level: 85 },
            { name: 'Friet', level: 80 }
        ]
    },
    {
        title: 'Muziek',
        icon: Settings,
        skills: [
            { name: 'Gitaar', level: 85 },
            { name: 'Piano', level: 70 },
            { name: 'Viool', level: 65 },
            { name: 'Keyboard', level: 60 }
        ]
    },
    {
        title: 'Wetenschap',
        icon: Laptop,
        skills: [
            { name: 'Mathematics', level: 100 },
            { name: 'Physics', level: 95 },
            { name: 'Chemistry', level: 90 },
            { name: 'Biology', level: 85 }
        ]
    }
]

const projects = [
    {
        title: 'Portfolio Website',
        description: 'Modern portfolio website built with Vue.js and Tailwind CSS',
        image: '/api/placeholder/800/400',
        technologies: ['Vue.js', 'Tailwind CSS', 'JavaScript']
    },
    {
        title: 'E-commerce Platform',
        description: 'Full-stack e-commerce solution with advanced features',
        image: '/api/placeholder/800/400',
        technologies: ['React', 'Node.js', 'MongoDB']
    }
]

const education = [
    {
        title: 'Student',
        institution: 'Laerskool Elspark',
        description: 'Eerste zeven jaar van school.',
        year: '2014-2021'
    },
    {
        title: 'Student',
        institution: 'Hoerskool Oosterlig',
        description: 'Mijn hogerschool.',
        year: '2021-2023'
    },
    {
        title: 'Student',
        institution: 'Jan van Brabant college Molenstraat',
        description: 'Mijn school op dit moment',
        year: '2024-present'
    }
]
</script>