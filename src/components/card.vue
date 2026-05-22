<template>
    <div class="2xl:mt-10 bg-neutral-primary-soft block max-w-sm xl:max-w-xl border rounded-md border-default rounded-base shadow-x duration-300 transition grayscale-100 hover:grayscale-0">
        <div>
            <img class="rounded-t-md h-57.5 w-full" :src="imageUrl" :alt="title" />
        </div>
        <div class="p-6 text-center">
            <span class="inline-flex items-center bg-brand-softer border border-brand-subtle text-fg-brand-strong text-xs font-light px-1.5 py-0.5 rounded-sm  tracking-wider">
                <svg 
                    class="w-3 h-3 me-1" 
                    aria-hidden="true" 
                    xmlns="http://www.w3.org/2000/svg" 
                    width="24" 
                    height="24" 
                    fill="none" 
                    viewBox="0 0 24 24">
                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18.122 17.645a7.185 7.185 0 0 1-2.656 2.495 7.06 7.06 0 0 1-3.52.853 6.617 6.617 0 0 1-3.306-.718 6.73 6.73 0 0 1-2.54-2.266c-2.672-4.57.287-8.846.887-9.668A4.448 4.448 0 0 0 8.07 6.31 4.49 4.49 0 0 0 7.997 4c1.284.965 6.43 3.258 5.525 10.631 1.496-1.136 2.7-3.046 2.846-6.216 1.43 1.061 3.985 5.462 1.754 9.23Z"/>
                </svg>
                {{ badge }}
            </span>
            <h5 class="uppercase mt-3 mb-6 text-2xl font-normal tracking-normal text-heading">{{ title }}</h5>
            <p class="mb-6 text-sm text-gray-500 leading-relaxed">
                {{ desc }}
            </p>
            <a 
                href="#" 
                class="inline-flex items-center text-white bg-black box-border border border-transparent rounded-sm hover:bg-brand-strong shadow-xs font-light tracking-widest leading-5 rounded-base text-sm px-4 py-2.5 focus:outline-none hover:bg-white hover:text-black hover:border-black duration-300 transition transform hover:-translate-y-0.5 hover:shadow-lg">
                Read more
                <svg class="w-4 h-4 ms-1.5 rtl:rotate-180 -me-0.5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24"><path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 12H5m14 0-4 4m4-4-4-4"/></svg>
            </a>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SkillCard',
    props: {
        image: {
            type: String,
            required: true
        },
        title: {
            type: String,
            required: true
        },
        badge: {
            type: String,
            required: true
        },
        desc: {
            type: String,
            required: true
        }
    },
    computed: {
        imageUrl() {
            // Construct absolute path from assets folder
            return new URL(`../assets/${this.image.split('/').pop()}`, import.meta.url).href
        }
    }
}
</script>
