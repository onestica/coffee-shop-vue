<script setup>
import IconChevronRight from "@/components/icons/IconChevronRight.vue"
defineProps(['medias'])
</script>

<template>
	<div id="carousel" class="flex flex-col justify-center items-center md:col-start-1 md:col-span-3 md:row-start-1">
        <div class="flex w-72 md:w-96 overflow-x-auto snap-x snap-mandatory scroll-smooth scrollbar-hide">
            <div v-for="media,index in medias" :key="index" :id="`media-${index+1}`" class="w-72 md:w-96 snap-start shrink-0">
                <img :src="media.path" alt="">
            </div>
        </div>
        <ul class="flex justify-center items-center gap-x-2">
            <li>
                <button>
                    <IconChevronRight :class="'rotate-180'" />
                </button>
            </li>
            <li v-for="media,index in medias" :key="index">
                <a :href="`#media-${index+1}`" class="block h-4 w-4 bg-neutral-200 rounded-full active:bg-neutral-300"></a>
            </li>
            <li>
                <button>
                    <IconChevronRight />
                </button>
            </li>
        </ul>
    </div>
</template>
