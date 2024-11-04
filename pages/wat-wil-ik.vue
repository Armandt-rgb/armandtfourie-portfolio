// pages/wat-wil-ik.vue
<template>
    <div class="min-h-screen bg-gradient-to-b from-gray-900 to-gray-800 pt-24 px-4 pb-12">
        <div class="max-w-7xl mx-auto">
            <!-- Hero Section -->
            <div class="text-center mb-16">
                <h1 class="text-4xl md:text-5xl font-bold text-white mb-4">
                    Wat wil ik?
                </h1>
                <p class="text-gray-400 text-lg max-w-2xl mx-auto">
                    Mijn visie, doelen en ambities voor de toekomst - waar ik naartoe wil en hoe ik dat wil bereiken.
                </p>
            </div>

            <!-- Vision Board Section -->
            <div class="mb-20">
                <h2 class="text-3xl font-bold text-white mb-8 text-center">Mijn Visie</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div v-for="(vision, index) in visionBoard" :key="index"
                        class="relative group bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 overflow-hidden">
                        <!-- Animated Background Gradient -->
                        <div
                            class="absolute inset-0 bg-gradient-to-r from-blue-500/10 to-purple-500/10 opacity-0 group-hover:opacity-100 transition-opacity duration-500">
                        </div>

                        <!-- Content -->
                        <div class="relative z-10">
                            <component :is="vision.icon"
                                class="w-12 h-12 text-blue-400 mb-4 transform group-hover:scale-110 transition-transform duration-300" />
                            <h3 class="text-xl font-semibold text-white mb-3">{{ vision.title }}</h3>
                            <p class="text-gray-400 group-hover:text-gray-300 transition-colors duration-300">
                                {{ vision.description }}
                            </p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Career Goals Timeline -->
            <div class="mb-20">
                <h2 class="text-3xl font-bold text-white mb-8 text-center">Carrière Doelen</h2>
                <div class="relative">
                    <!-- Timeline Line -->
                    <div class="absolute left-0 md:left-1/2 h-full w-0.5 bg-blue-500/30 transform -translate-x-1/2">
                    </div>

                    <div class="space-y-16">
                        <div v-for="(goal, index) in careerGoals" :key="index" class="relative">
                            <!-- Timeline Item -->
                            <div :class="[
                                'flex flex-col md:flex-row gap-8 items-center md:items-start',
                                index % 2 === 0 ? 'md:flex-row-reverse' : ''
                            ]">
                                <!-- Timeline Point -->
                                <div
                                    class="absolute left-0 md:left-1/2 w-4 h-4 bg-blue-500 rounded-full transform -translate-x-1/2 mt-2">
                                </div>

                                <!-- Content -->
                                <div
                                    class="md:w-1/2 bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 hover:shadow-xl hover:shadow-blue-500/10 transition-all duration-300">
                                    <span class="text-blue-400 text-sm font-semibold">{{ goal.timeframe }}</span>
                                    <h3 class="text-xl font-semibold text-white mt-2 mb-3">{{ goal.title }}</h3>
                                    <p class="text-gray-400">{{ goal.description }}</p>
                                    <div class="flex flex-wrap gap-2 mt-4">
                                        <span v-for="skill in goal.requiredSkills" :key="skill"
                                            class="px-3 py-1 text-sm text-blue-300 bg-blue-500/10 rounded-full">
                                            {{ skill }}
                                        </span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Personal Development Goals -->
            <div class="mb-20">
                <h2 class="text-3xl font-bold text-white mb-8 text-center">Persoonlijke Ontwikkeling</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div v-for="(goal, index) in personalGoals" :key="index"
                        class="bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 transform hover:-translate-y-2 transition-all duration-300">
                        <div class="flex items-center justify-between mb-4">
                            <component :is="goal.icon" class="w-8 h-8 text-blue-400" />
                            <span :class="[
                                'px-3 py-1 text-sm rounded-full',
                                `text-${goal.priority.color}-300 bg-${goal.priority.color}-500/10`
                            ]">
                                {{ goal.priority.label }}
                            </span>
                        </div>
                        <h3 class="text-xl font-semibold text-white mb-3">{{ goal.title }}</h3>
                        <p class="text-gray-400">{{ goal.description }}</p>
                        <!-- Progress Bar -->
                        <div class="mt-4">
                            <div class="flex justify-between text-sm mb-1">
                                <span class="text-gray-400">Voortgang</span>
                                <span class="text-blue-400">{{ goal.progress }}%</span>
                            </div>
                            <div class="h-2 bg-gray-700 rounded-full overflow-hidden">
                                <div class="h-full bg-gradient-to-r from-blue-500 to-purple-500 rounded-full transition-all duration-1000 ease-out"
                                    :style="{ width: `${goal.progress}%` }"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Inspiration Quote -->
            <div class="text-center max-w-4xl mx-auto">
                <blockquote class="text-2xl text-gray-300 italic">
                    "{{ inspirationalQuote.text }}"
                    <footer class="text-gray-400 mt-4 text-lg">— {{ inspirationalQuote.author }}</footer>
                </blockquote>
            </div>
        </div>
    </div>
</template>

<script setup>
import {
    Rocket,
    Target,
    Trophy,
    BookOpen,
    Globe,
    Brain,
    Heart,
    Users,
    Lightbulb
} from 'lucide-vue-next'

const visionBoard = [
    {
        icon: Rocket,
        title: 'Innovatie Leiden',
        description: 'Streven naar leidende posities in innovatieve technologieprojecten en het vormgeven van de toekomst van digitale oplossingen.'
    },
    {
        icon: Globe,
        title: 'Internationale Ervaring',
        description: 'Werken aan internationale projecten en samenwerken met diverse teams wereldwijd om mijn horizon te verbreden.'
    },
    {
        icon: Brain,
        title: 'Continu Leren',
        description: 'Blijven groeien door het leren van nieuwe technologieën en het ontwikkelen van nieuwe vaardigheden.'
    }
]

const careerGoals = [
    {
        timeframe: 'Korte termijn (1-2 jaar)',
        title: 'Senior Developer Positie',
        description: 'Doorgroeien naar een senior ontwikkelaar rol met focus op architectuur en teamleiding.',
        requiredSkills: ['Team Leadership', 'System Design', 'Architecture']
    },
    {
        timeframe: 'Middellange termijn (2-4 jaar)',
        title: 'Tech Lead',
        description: 'Leiding geven aan een ontwikkelteam en verantwoordelijk zijn voor technische beslissingen.',
        requiredSkills: ['Project Management', 'Mentoring', 'Strategic Planning']
    },
    {
        timeframe: 'Lange termijn (5+ jaar)',
        title: 'Technisch Directeur',
        description: 'Strategische technische visie ontwikkelen en implementeren voor grote projecten.',
        requiredSkills: ['Leadership', 'Innovation', 'Strategy']
    }
]

const personalGoals = [
    {
        icon: BookOpen,
        title: 'Masteren van AI/ML',
        description: 'Diepgaande kennis ontwikkelen in AI en Machine Learning technieken.',
        priority: { label: 'Hoog', color: 'red' },
        progress: 5
    },
    {
        icon: BookOpen,
        title: 'Masteren van Full-Stack Development',
        description: 'Junior developers begeleiden en kennis delen binnen de community.',
        priority: { label: 'Medium', color: 'yellow' },
        progress: 30
    },
    {
        icon: Heart,
        title: 'Personal Leadership',
        description: 'Gezonde balans tussen werk en privéleven maintainen.',
        priority: { label: 'Hoog', color: 'red' },
        progress: 45
    }
]

const inspirationalQuote = {
    text: 'The only way to do great work is to love what you do.',
    author: 'Steve Jobs'
}
</script>