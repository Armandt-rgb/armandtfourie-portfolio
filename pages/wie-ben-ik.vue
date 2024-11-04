<template>
    <div class="min-h-screen bg-gradient-to-b from-gray-900 to-gray-800 pt-24 px-4 pb-12">
        <div class="max-w-7xl mx-auto">
            <!-- Hero Section -->
            <div class="text-center mb-16">
                <div class="relative inline-block">
                    <img src="/images/logo.png" alt="Armandt Fourie"
                        class="w-32 h-32 rounded-full border-4 border-emerald-500/30 mb-6 hover:scale-105 transition-transform duration-300" />
                    <div class="absolute -bottom-2 -right-2 bg-emerald-500 text-white px-3 py-1 rounded-full text-sm">
                        Available for work
                    </div>
                </div>
                <h1 class="text-4xl md:text-5xl font-bold text-white mb-4">
                    Wie ben ik?
                </h1>
                <p class="text-gray-400 text-lg max-w-2xl mx-auto">
                    Een reis door mijn verhaal, interesses en wat mij maakt tot wie ik ben.
                </p>
            </div>

            <!-- Quick Facts -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-16">
                <div v-for="fact in quickFacts" :key="fact.label"
                    class="bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 flex items-center space-x-4 hover:bg-gray-800/70 transition-all duration-300">
                    <component :is="fact.icon" class="w-8 h-8 text-emerald-500" />
                    <div>
                        <h3 class="text-white font-medium">{{ fact.label }}</h3>
                        <p class="text-gray-400">{{ fact.value }}</p>
                    </div>
                </div>
            </div>

            <!-- Personal Story Timeline -->
            <div class="mb-20">
                <h2 class="text-3xl font-bold text-white mb-12 text-center">Mijn Reis</h2>
                <div class="relative">
                    <!-- Timeline Line -->
                    <div class="absolute left-0 md:left-1/2 h-full w-0.5 bg-emerald-500/30 transform -translate-x-1/2">
                    </div>

                    <div class="space-y-16">
                        <div v-for="(event, index) in timeline" :key="index" class="relative">
                            <div :class="[
                                'flex flex-col md:flex-row gap-8 items-start',
                                index % 2 === 0 ? 'md:flex-row-reverse' : ''
                            ]">
                                <!-- Timeline Point -->
                                <div
                                    class="absolute left-0 md:left-1/2 w-4 h-4 bg-emerald-500 rounded-full transform -translate-x-1/2 mt-2">
                                </div>

                                <!-- Content -->
                                <div class="md:w-1/2">
                                    <div
                                        class="bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 hover:shadow-xl hover:shadow-emerald-500/10 transition-all duration-300">
                                        <span class="text-emerald-400 text-sm font-semibold">{{ event.year }}</span>
                                        <h3 class="text-xl font-semibold text-white mt-2 mb-3">{{ event.title }}</h3>
                                        <p class="text-gray-400">{{ event.description }}</p>
                                        <img v-if="event.image" :src="event.image" :alt="event.title"
                                            class="w-full h-48 object-cover rounded-lg mt-4 hover:scale-105 transition-transform duration-300" />
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Interests & Hobbies -->
            <div class="mb-20">
                <h2 class="text-3xl font-bold text-white mb-8 text-center">Interesses & Hobbies</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div v-for="(category, index) in interests" :key="index"
                        class="bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 group hover:-translate-y-2 transition-all duration-300">
                        <div class="flex items-center space-x-4 mb-6">
                            <component :is="category.icon"
                                class="w-8 h-8 text-emerald-500 group-hover:scale-110 transition-transform duration-300" />
                            <h3 class="text-xl font-semibold text-white">{{ category.title }}</h3>
                        </div>
                        <div class="space-y-4">
                            <div v-for="item in category.items" :key="item.name"
                                class="flex items-center justify-between">
                                <span class="text-gray-300">{{ item.name }}</span>
                                <div class="flex">
                                    <component :is="Star" v-for="n in 5" :key="n" :class="[
                                        'w-4 h-4',
                                        n <= item.rating ? 'text-emerald-500' : 'text-gray-600'
                                    ]" />
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Personal Values -->
            <!-- Personal Values Section -->
<div class="mb-20">
  <h2 class="text-3xl font-bold text-white mb-8 text-center">Mijn kwaliteiten</h2>
  
  <!-- Qualities Grid -->
  <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
  <!-- First Column -->
  <div class="space-y-8">
    <div 
      v-for="(quality, index) in qualities.slice(0, Math.ceil(qualities.length / 2))"
      :key="quality.title"
      class="bg-gray-800/50 backdrop-blur-sm rounded-xl overflow-hidden hover:shadow-xl hover:shadow-emerald-500/10 transition-all duration-300"
    >
      <!-- Quality Header -->
      <div 
        class="bg-emerald-500/10 p-6 flex items-center space-x-4 cursor-pointer"
        @click="quality.isOpen = !quality.isOpen"
      >
        <component 
          :is="quality.icon" 
          class="w-6 h-6 text-emerald-500"
        />
        <h3 class="text-xl font-semibold text-white">{{ quality.title }}</h3>
        <ChevronDown 
          class="w-5 h-5 text-emerald-500 ml-auto transform transition-transform duration-300"
          :class="{ 'rotate-180': quality.isOpen }"
        />
      </div>

      <!-- Quality Content -->
      <div 
        v-show="quality.isOpen"
        class="p-6 space-y-4"
      >
        <!-- Fit -->
        <div>
          <h4 class="text-emerald-400 font-medium mb-2">Past dit bij me?</h4>
          <p class="text-gray-300">{{ quality.fit }}</p>
        </div>

        <!-- Categories -->
        <div 
          v-for="category in ['valkuil', 'allergie', 'uitdaging']" 
          :key="category"
          class="bg-gray-900/30 rounded-lg p-4"
        >
          <h4 class="text-emerald-400 font-medium capitalize mb-2">{{ category }}</h4>
          <p class="text-gray-300">{{ quality[category] }}</p>
        </div>
      </div>
    </div>
  </div>

  <!-- Second Column -->
  <div class="space-y-8">
    <div 
      v-for="(quality, index) in qualities.slice(Math.ceil(qualities.length / 2))"
      :key="quality.title"
      class="bg-gray-800/50 backdrop-blur-sm rounded-xl overflow-hidden hover:shadow-xl hover:shadow-emerald-500/10 transition-all duration-300"
    >
      <!-- Quality Header -->
      <div 
        class="bg-emerald-500/10 p-6 flex items-center space-x-4 cursor-pointer"
        @click="quality.isOpen = !quality.isOpen"
      >
        <component 
          :is="quality.icon" 
          class="w-6 h-6 text-emerald-500"
        />
        <h3 class="text-xl font-semibold text-white">{{ quality.title }}</h3>
        <ChevronDown 
          class="w-5 h-5 text-emerald-500 ml-auto transform transition-transform duration-300"
          :class="{ 'rotate-180': quality.isOpen }"
        />
      </div>

      <!-- Quality Content -->
      <div 
        v-show="quality.isOpen"
        class="p-6 space-y-4"
      >
        <!-- Fit -->
        <div>
          <h4 class="text-emerald-400 font-medium mb-2">Past dit bij me?</h4>
          <p class="text-gray-300">{{ quality.fit }}</p>
        </div>

        <!-- Categories -->
        <div 
          v-for="category in ['valkuil', 'allergie', 'uitdaging']" 
          :key="category"
          class="bg-gray-900/30 rounded-lg p-4"
        >
          <h4 class="text-emerald-400 font-medium capitalize mb-2">{{ category }}</h4>
          <p class="text-gray-300">{{ quality[category] }}</p>
        </div>
      </div>
    </div>
  </div>
</div>
</div>

            <!-- Fun Facts -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-20">
                <div v-for="(fact, index) in funFacts" :key="index"
                    class="bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 hover:bg-gray-800/70 transition-all duration-300">
                    <h3 class="text-lg font-semibold text-white mb-4 flex items-center">
                        <Sparkles class="w-5 h-5 text-emerald-500 mr-2" />
                        {{ fact.title }}
                    </h3>
                    <p class="text-gray-400">{{ fact.description }}</p>
                </div>
            </div>

            <!-- Contact Section -->
            <div class="text-center">
                <h2 class="text-3xl font-bold text-white mb-6">Laten we connecten</h2>
                <p class="text-gray-400 mb-8 max-w-2xl mx-auto">
                    Altijd geïnteresseerd in nieuwe connecties en mogelijkheden om samen te werken.
                </p>
                <div class="flex justify-center space-x-6">
                    <a v-for="social in socials" :key="social.name" :href="social.url" target="_blank"
                        rel="noopener noreferrer"
                        class="text-gray-400 hover:text-emerald-500 transition-colors duration-300">
                        <component :is="social.icon" class="w-8 h-8" />
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import {
    MapPin,
    Calendar,
    Briefcase,
    GraduationCap,
    Music,
    Film,
    Utensils,
    Book,
    Heart,
    Star,
    Sparkles,
    Github,
    Linkedin,
    Mail,
    Camera,
    Trophy,
    Users,
    Lightbulb,
    Ear, // for Listening
    Target, // for Goal-oriented
    HeartHandshake, // for Honest
    Brain, // for Self-aware
    
    ChevronDown, // Added this import
    Shield // for Assertive

} from 'lucide-vue-next'

const quickFacts = [
    { label: 'Locatie', value: 'Helmond', icon: MapPin },
    { label: 'Geboren', value: 'Alberton', icon: MapPin },
    { label: 'Werk', value: 'Developer', icon: Briefcase },
    { label: 'Opleiding', value: 'Hoërskool Oosterlig', icon: GraduationCap }
]

const timeline = [
    {
        year: 'Geboren',
        title: 'Alberton, Zuid-Afrika',
        description: 'Geboren in Alberton, een stad die me altijd een gevoel van verbondenheid heeft gegeven.',
        image: 'Alberton.jpg'
    },
    {
        year: 'Basisschool',
        title: 'Laerskool Elspark',
        description: 'Mijn basisschooltijd bracht ik door op Laerskool Elspark, een tijd waar ik met veel plezier op terugkijk.',
        image: '9.png'
    },
    {
        year: 'Middelbare School',
        title: 'Hoërskool Oosterlig',
        description: 'Ontwikkelde mijn interesses in Afrikaans en Grafisch ontwerp.',
        image: 'highschool.jpeg'
    },
    {
        year: 'Heden',
        title: 'Helmond, Nederland',
        description: 'Momenteel woonachtig in Helmond, waar ik mijn carrière verder ontwikkel.',
        image: 'helmond.jpeg'
    }
]

const interests = [
    {
        title: 'Muziek',
        icon: Music,
        items: [
            { name: 'Blues Rock', rating: 5 },
            { name: 'Klassiek', rating: 4 },
            { name: 'R&B', rating: 4 }
        ]
    },
    {
        title: 'Films',
        icon: Film,
        items: [
            { name: 'Rocky 4', rating: 5 },
            { name: 'Drama', rating: 4 },
            { name: 'Komedie', rating: 3 }
        ]
    },
    {
        title: 'Keuken',
        icon: Utensils,
        items: [
            { name: 'Italiaans', rating: 5 },
            { name: 'Risotto', rating: 5 },
            { name: 'Pasta', rating: 4 }
        ]
    }
]
const qualities = reactive([
    {
        title: 'Luisterend',
        icon: Ear,
        isOpen: true,
        fit: 'Ja, ik luister goed naar anderen om ze echt te begrijpen voordat ik reageer. Dit helpt me om beter met mensen om te gaan.',
        valkuil: 'Soms luister ik te veel en vergeet ik mijn eigen mening te delen.',
        allergie: 'Ik kan niet goed omgaan met mensen die niet luisteren of constant onderbreken.',
        uitdaging: 'Meer mijn eigen mening naar voren brengen, ook als ik bezig ben met luisteren.'
    },
    {
        title: 'Doelgericht',
        icon: Target,
        isOpen: false,
        fit: 'Ja, ik stel graag doelen en werk hard om die te bereiken. Ik houd ervan om resultaat te zien.',
        valkuil: 'Soms ben ik te gefocust op het doel en mis ik betere alternatieven of nieuwe ideeën.',
        allergie: 'Ik heb moeite met mensen die traag werken of geen duidelijke doelen hebben.',
        uitdaging: 'Leren geduldiger te zijn en meer waarde hechten aan het proces, niet alleen het eindresultaat.'
    },
    {
        title: 'Eerlijk',
        icon: HeartHandshake,
        isOpen: false,
        fit: 'Ja, ik ben altijd eerlijk en open, ook al kan dat soms moeilijk zijn.',
        valkuil: 'Mijn eerlijkheid kan soms te direct zijn en anderen kwetsen zonder dat ik dat bedoel.',
        allergie: 'Ik kan niet goed omgaan met oneerlijkheid of leugens.',
        uitdaging: 'Mijn eerlijkheid combineren met tact en begrip voor anderen.'
    },
    {
        title: 'Zelfbewust',
        icon: Brain,
        isOpen: false,
        fit: 'Ja, ik ben zelfbewust en ken mijn sterke en zwakke punten goed.',
        valkuil: 'Ik kan te streng voor mezelf zijn als ik niet aan mijn eigen verwachtingen voldoe.',
        allergie: 'Ik erger me aan mensen die geen zelfinzicht hebben en niet openstaan voor feedback.',
        uitdaging: 'Milder voor mezelf zijn en accepteren dat fouten maken bij het leren hoort.'
    },
    {
        title: 'Assertief (Weerbaar)',
        icon: Shield,
        isOpen: false,
        fit: 'Ja, ik kom op voor mezelf en geef mijn grenzen duidelijk aan.',
        valkuil: 'Mijn assertiviteit kan soms te sterk overkomen, waardoor het lijkt alsof ik eigenwijs ben.',
        allergie: 'Ik heb moeite met mensen die zich laten ondersneeuwen en niet voor zichzelf opkomen.',
        uitdaging: 'Mijn assertiviteit afstemmen op de situatie, zodat het passend en vriendelijk blijft.'
    },
    {
        title: 'Creatief',
        icon: Lightbulb,
        isOpen: false,
        fit: 'Ja, ik ben creatief en vind het leuk om nieuwe ideeën te bedenken en uit te werken.',
        valkuil: 'Soms ben ik te veel bezig met creatieve oplossingen en vergeet ik de praktische kant.',
        allergie: 'Ik kan niet goed omgaan met starre denkers die geen ruimte geven aan creativiteit.',
        uitdaging: 'Meer balans vinden tussen creativiteit en realisme, zodat ideeën ook uitvoerbaar zijn.'
    }
])

const funFacts = [
    {
        title: 'Favoriete Artiest',
        description: 'Howlin\' Wolf heeft een speciale plek in mijn muzikale hart.'
    },
    {
        title: 'Hobby',
        description: 'Een grote passie voor jachten en watersport.'
    },
    {
        title: 'Sport',
        description: 'Tennis is mijn favoriete manier om actief te blijven.'
    },
    {
        title: 'Reizen',
        description: 'Heb in verschillende steden gewoond, waaronder Heidelberg en Boksburg.'
    }
]

const socials = [
    { name: 'GitHub', url: 'https://github.com/Armandt-rgb', icon: Github },
    { name: 'Email', url: 'mailto:115021@jvbcollege.nl', icon: Mail }
]
</script>