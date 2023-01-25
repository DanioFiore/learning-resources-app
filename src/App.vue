<template>
    <ul>
        <learning-resource v-for="resource in storedResources" :key="resource.id" :id="resource.id" :title="resource.title" :description="resource.description" :link="resource.link"></learning-resource>
    </ul>
</template>

<script>
import LearningResource from './components/learning-resources/LearningResource.vue';

export default {
    components: {
        LearningResource,
    },
    data() {
        return {
            storedResources: [
                {
                    id: 'vue-guide',
                    title: 'Vue Official Guide',
                    description: 'The official guide of vue.js',
                    link: 'https://vuejs.org',
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to google',
                    link: 'https://google.com',
                }
            ]
        }
    }
}
</script>
