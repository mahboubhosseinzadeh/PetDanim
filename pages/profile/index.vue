<template>
    <section>
        <div class="loading-box" v-if="loading == true">
            <div class="loader" ></div>
        </div>
        <Home 
        :statistics="statistics"
        v-else />
    </section>
</template>


<script setup>
import {usePetdanimStore} from '~/store/petdanimStore'
import Home from "@/components/Dashboard/Home.vue";
import {storeToRefs} from 'pinia'
const petdanimStore = usePetdanimStore()

const {authUser} = storeToRefs(petdanimStore)
const loading = ref(true)
const reciveStatus = ref(true)
const statistics = ref(null)

definePageMeta({
  layout: 'user-profile',  
  middleware: 'user-auth'
})


onMounted(() => {
    getStatistics()
})


const getStatistics = async () => {
    loading.value = true

    const result = await petdanimStore.getUserStatistics()
    if(result != false && result.status == 200) {
        loading.value = false
        statistics.value = result.result
    }else {
        loading.value = false
        reciveStatus.value = false
    }
}
</script>

<style scoped>
/* HTML: <div class="loader"></div> */
.loader {
  width: 50px;
  aspect-ratio: 1;
  border-radius: 50%;
  background: 
    radial-gradient(farthest-side,#f97316 94%,#0000) top/8px 8px no-repeat,
    conic-gradient(#0000 30%,#f97316);
  -webkit-mask: radial-gradient(farthest-side,#0000 calc(100% - 8px),#000 0);
  animation: l13 1s infinite linear;
}
@keyframes l13{ 
  100%{transform: rotate(1turn)}
}

.loading-box{
    width: 100%;
    height:600px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;

    background: #f9f9f9;
    background: linear-gradient(110deg, #ececec 8%, #f5f5f5 18%, #ececec 33%);
    border-radius: 5px;
    background-size: 200% 100%;
    -webkit-animation: .5s shine linear infinite;
            animation: .5s shine linear infinite;
}

@-webkit-keyframes shine {
  to {
    background-position-x: -200%;
  }
}

@keyframes shine {
  to {
    background-position-x: -200%;
  }
}
</style>

