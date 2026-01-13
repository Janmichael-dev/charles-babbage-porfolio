<template>
	<!-- My Projects -->
            <section class="pb-5" id="projects">
                    <h1 class="mt-5 mb-5 pb-4 text-center">My Projects</h1>
                <!-- Nasted Loop -->
                <!-- [[1,2,3],[4,5,6],[7,8,9]] -->
                <div
                    v-for = "(group, index) in chunkedProjects"
                    :key = "index"
                    class = "card-deck my-5 justify-content-center"

                >
                    <ProjectCard
                    v-for  ="project in group"
                    :key= "project.id"
                    :project = "project"
                        />              
                </div>






            </section>
</template>

<script setup>
    // computed function form vue to define reactive derived state
    import {computed} from 'vue';
    import ProjectCard from './ProjectCard.vue';
    import projects from '../data/project.json';

    const chunkSize = 3;


    //Create a computed property that splits the projects into smaller arrays ("chunks")
    // Each chunk will contain up to the number of the 'chunkSize' number of the projects
    // This allows us to group them visually in separate rows in the UI

    const chunkedProjects = computed (() => {
        const chunks =[];
        for ( let i =0; i <  projects.length; i += chunkSize){
            chunks.push(projects.slice(i, i + chunkSize));
        }
        return chunks
    })

</script>