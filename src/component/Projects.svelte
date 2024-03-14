<script lang="ts">
    import {  slide } from "svelte/transition";
    import projects from "../lib/projectsData";
    import { onMount } from 'svelte';

    let currentProjectIndex = 0;

    function nextProject() {
        currentProjectIndex = (currentProjectIndex + 1) % projects.length;
    }

    function prevProject() {
        currentProjectIndex =
            (currentProjectIndex - 1 + projects.length) % projects.length;
    }

    onMount(() => {
        const interval = setInterval(nextProject, 4000); 

        return () => {
            clearInterval(interval); 
        };
    });
</script>

<div class="gradient"></div>

<div class="section-black">
  <section id="projects">
    <h2>Projects I'm proud of</h2>
    <div class="slider-container">
      {#each projects as project, index}
        {#if index === currentProjectIndex}
          <article in:slide={{ duration: 300 }}>
            <div class="text">
              <h4>Latest Project</h4>
              <h3>{project.title}</h3>
              <p class="blackbox">
                {project.description}

                {#if project.github}
                  <a href={project.github}>
                    <a target="_blank" rel="noopener" href={project.github}>
                      <span class="fab fa-github-alt" aria-hidden="true"></span>
                      <span class="sr-only">Github</span></a
                    >
                  </a>
                {/if}

                {#if project.demo}
                  <a href={project.demo}>
                    <a target="_blank" rel="noopener" href={project.demo}>
                      <span class="fas fa-external-link-alt" aria-hidden="true"
                      ></span>
                      <span class="sr-only">Demo</span></a
                    >
                  </a>
                {/if}
              </p>
              <h4>Technologies used include:</h4>
              <ul>
                {#each project.technologies ?? [] as technology}
                  <li>{technology}</li>
                {/each}
              </ul>
            </div>

            <div class="project--img">

                <img src={project.image} alt={project.title} />
            </div>
          </article>
        {/if}
      {/each}

      <button class="button" on:click={prevProject}>Previous</button>
      <button class="button" on:click={nextProject}>Next</button>
    </div>
  </section>
</div>

<style>
  .project--img {
    height: 700px;
  }

  .project--img img{
  
    height: 100%;
    object-fit: cover;
  }

  button{
    border: none;
    cursor: pointer;
  }


</style>
