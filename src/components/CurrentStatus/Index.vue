<template>
    <div class="container w-9/12 mx-auto mt-12 bg-white rounded-lg p-2">
        <span class="pl-3 py-4 font-bold inline-block">Current server status</span>
        <img
            src="https://raw.githubusercontent.com/MohsenAbrishami/monitoring-panel/main/src/assets/refresh.png"
            class="w-10 inline-block float-right mr-3 cursor-pointer"
            @click.prevent="getCurrentStatus()"
        >

        <div v-if="isLoading" class="loader" />
        <div v-else class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-5 gap-4">
            <StatusItem
                title="Cpu Usage"
                :result="statuses.memory"
                color="bg-blue-100"
                icon="https://raw.githubusercontent.com/MohsenAbrishami/monitoring-panel/main/src/assets/cpu-icon.png"
            />
            <StatusItem
                title="Memory Usage"
                :result="statuses.memory"
                color="bg-green-100"
                icon="https://raw.githubusercontent.com/MohsenAbrishami/monitoring-panel/main/src/assets/ram-icon.png"
            />
            <StatusItem
                title="Hard Disk Space"
                :result="statuses.memory"
                color="bg-red-100"
                icon="https://raw.githubusercontent.com/MohsenAbrishami/monitoring-panel/main/src/assets/harddisk-icon.png"
            />
            <StatusItem
                title="Web server status"
                :result="statuses.memory"
                color="bg-purple-100"
                icon="https://raw.githubusercontent.com/MohsenAbrishami/monitoring-panel/main/src/assets/web-server-icon.png"
            />
            <StatusItem
                title="Network Status"
                :result="statuses.memory"
                color="bg-yellow-100"
                icon="https://raw.githubusercontent.com/MohsenAbrishami/monitoring-panel/main/src/assets/network-icon.png"
            />
        </div>
    </div>
</template>

<script setup>
import {
    onBeforeUnmount, onMounted, reactive, ref
} from 'vue'
import axios from 'axios'
import StatusItem from './StatusItem.vue'

const statuses = reactive({
    cpu: 'Loading..',
    hardDisk: 'Loading..',
    memory: 'Loading..',
    network: 'Loading..',
    webServer: 'Loading..',
})

const isLoading = ref(false)

onMounted(() => {
    getCurrentStatus()
})

onBeforeUnmount(() => {
    clearInterval(statusChecker)
})

const statusChecker = setInterval(() => {
    getCurrentStatus()
}, 180000)

function getCurrentStatus() {
    isLoading.value = true
    axios.get('monitor/current')
        .then((value) => {
            statuses.cpu = `${Number(value.data.cpu).toFixed(2)} %`
            statuses.hardDisk = `${(Number(value.data.hard_disk) / (1024 ** 3)).toFixed(2)} GB`
            statuses.memory = `${Number(value.data.memory).toFixed(2)} %`
            statuses.network = value.data.network
            statuses.webServer = value.data.web_server
            isLoading.value = false
        })
}
</script>

<style scoped>
.loader {
  border: 16px solid #f3f3f3;
  border-radius: 50%;
  border-top: 16px solid #3498db;
  width: 120px;
  height: 120px;
  -webkit-animation: spin 2s linear infinite; /* Safari */
  animation: spin 2s linear infinite;

  margin-left: auto;
  margin-right: auto;
  display: block;
}

/* Safari */
@-webkit-keyframes spin {
  0% { -webkit-transform: rotate(0deg); }
  100% { -webkit-transform: rotate(360deg); }
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
