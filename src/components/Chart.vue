<template>
    <div class="w-9/12 bg-white my-5 mx-auto p-5 rounded-lg">
        <VueDatePicker
            v-model="date"
            range
            auto-apply
            :enable-time-picker="false"
            :format="'yyyy/MM/dd'"
        />
        <div class="w-2/12 inline-block float-left pt-16">
            <div class="block pt-2">
                <input
                    v-model="resources.cpu"
                    type="checkbox"
                    @click="generateChart('cpu')"
                >
                <span class="text-blue-500 font-bold mx-4">CPU</span>
            </div>
            <div class="block pt-2">
                <input
                    v-model="resources.memory"
                    type="checkbox"
                    @click="generateChart('memory')"
                >
                <span class="text-green-500 font-bold mx-4">Memory</span>
            </div>
            <div class="block pt-2">
                <input
                    v-model="resources.hardDisk"
                    type="checkbox"
                    @click="generateChart('hardDisk')"
                >
                <span class="text-red-500 font-bold mx-4">HDD</span>
            </div>
            <div class="block pt-2">
                <input
                    v-model="resources.webServer"
                    type="checkbox"
                    @click="generateChart('webServer')"
                >
                <span class="text-emerald-400 font-bold mx-4">Web Server</span>
            </div>
            <div class="block pt-2">
                <input
                    v-model="resources.network"
                    type="checkbox"
                    @click="generateChart('network')"
                >
                <span class="text-purple-400 font-bold mx-4">Network</span>
            </div>
        </div>
        <div class="w-10/12 inline-block h-80">
            <Line :data="data" :options="options" />
        </div>
    </div>
</template>

<script setup>
import {
    Chart as ChartJS,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend
} from 'chart.js'
import { Line } from 'vue-chartjs'
import { onMounted, reactive, ref } from 'vue'
import axios from 'axios'
import VueDatePicker from '@vuepic/vue-datepicker'
import '@vuepic/vue-datepicker/dist/main.css'

ChartJS.register(
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend
)

const data = ref({})

const date = ref()

const options = {
    responsive: true,
    maintainAspectRatio: false,
}

const resourceLog = reactive({
    history: null,
})

const resources = reactive({
    cpu: true,
    memory: true,
    hardDisk: true,
    webServer: true,
    network: true,
})

function getResourceLogHistories() {
    axios.get('http://localhost:8000/monitor/history/2023-03-14/2023-03-26')
        .then((value) => {
            resourceLog.history = value.data
            generateChart()
        })
}

function generateChart(key) {
    resources[key] = !resources[key]

    data.value = {
        labels: resourceLog.history?.labels,
        datasets: [],
    }

    if (resources.cpu) {
        data.value.datasets.push({
            label: 'CPU',
            backgroundColor: '#60a5fa',
            data: resourceLog.history?.resource_log_count.cpu,
        })
    }

    if (resources.memory) {
        data.value.datasets.push({
            label: 'Memory',
            backgroundColor: '#4ade80',
            data: resourceLog.history?.resource_log_count.memory,
        })
    }

    if (resources.hardDisk) {
        data.value.datasets.push({
            label: 'hdd',
            backgroundColor: '#f87171',
            data: resourceLog.history?.resource_log_count.hard_disk,
        })
    }

    if (resources.webServer) {
        data.value.datasets.push({
            label: 'web_server',
            backgroundColor: '#34d399',
            data: resourceLog.history?.resource_log_count.network,
        })
    }

    if (resources.network) {
        data.value.datasets.push({
            label: 'network',
            backgroundColor: '#c084fc',
            data: resourceLog.history?.resource_log_count.web_server,
        })
    }
}

function setInitializeDate() {
    const endDate = new Date()
    const startDate = new Date(new Date().setDate(endDate.getDate() - 7))
    date.value = [startDate, endDate]
}

onMounted(() => {
    getResourceLogHistories()
    setInitializeDate()
})

generateChart()
</script>
