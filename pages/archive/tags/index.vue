<template>
    <div class="bg-slate-100 dark:bg-dark-900">
        <Loading :isShow="showLoading" />
        <BlogSection class="dark:!bg-dark-900/30 bg-gray-50 py-16 lg:py-16">
            <HeaderSection icon="list" title="هشتگ ها" />
            <Grid class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-4">
                <contentTag 
                v-if="showLoading == false && tagsList.length != 0"
                :tags="tagsList"/>
            </Grid>
        </BlogSection>
    </div>
</template>

<script setup>
import Loading from '@/components/Loading/index.vue'
import BlogSection from "@/components/TemplateParts/Section/BlogSection.vue";
import HeaderSection from "@/components/TemplateParts/Header/header.vue";
import Grid from "@/components/TemplateParts/Grid/Grid.vue";
import contentTag from "@/components/TemplateParts/contentTag.vue";

const {appBaseUrl} = useRuntimeConfig().public
const tagsList = ref([])
const showLoading = ref(true)

const getTags = async () => {
    const {data} = await useFetch(`${appBaseUrl}/api/mag/tags/get-all`)
    if(data.value.status == 200) {
        setTimeout(() => {
            showLoading.value = false
        }, 500);
        tagsList.value = data.value.result
    }
}

getTags()
</script>
