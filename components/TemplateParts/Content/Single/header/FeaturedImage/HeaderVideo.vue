<template>
            <div class="relative lg:w-8/12 flex-shrink-0">
            <div
                class="aspect-w-16  aspect-h-9 border-4 border-neutral-300 dark:border-neutral-800 shadow-2xl bg-neutral-800 rounded-3xl overflow-hidden z-0">
                <div>
                    <div class="lg:absolute inset-0 w-full h-full">
                        <div class="w-full h-full">
                            <video class="w-full object-cover h-full" controls>
                                <source :src="`${appBaseUrl}/storage/${postData.post.video.video_path}`">
                                <!-- <source src="mov_bbb.ogg" type="video/ogg"> -->
                                Your browser does not support HTML video.
                            </video>
                        </div>
                    </div>
                </div>
            </div>
        </div>
</template>

<script setup>
import {usePetdanimStore} from '@/store/petdanimStore.js'
import {storeToRefs} from 'pinia'

const {appBaseUrl} = useRuntimeConfig().public
const petdanimStore = usePetdanimStore()
const {postData} = storeToRefs(petdanimStore)
</script>