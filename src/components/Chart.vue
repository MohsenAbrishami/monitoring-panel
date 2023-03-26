<template>
    <div class="w-9/12 bg-white my-5 mx-auto p-5 rounded-lg">
        <div class="w-2/12 inline-block float-left pt-10">
            <button
                class="w-32 bg-blue-400 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                @click="generateChart()"
            >
                CPU
            </button>
            <button
                class="w-32 bg-green-400 hover:bg-green-700 text-white font-bold py-2 px-4 rounded mt-3"
                @click="generateChart()"
            >
                Memory
            </button>
            <button
                class="w-32 bg-red-400 hover:bg-red-700 text-white font-bold py-2 px-4 rounded mt-3"
                @click="generateChart()"
            >
                HDD
            </button>
            <button
                class="w-32 bg-emerald-400 hover:bg-emerald-700 text-white font-bold py-2 px-4 rounded mt-3"
                @click="generateChart()"
            >
                Web Server
            </button>
            <button
                class="w-32 bg-purple-400 hover:bg-purple-700 text-white font-bold py-2 px-4 rounded mt-3"
                @click="generateChart()"
            >
                Network
            </button>
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

const options = {
    responsive: true,
    maintainAspectRatio: false,
}

const resourceLog = reactive({
    history: null,
})

function getResourceLogHistories() {
    axios.get('http://localhost:8000/monitor/history/2023-03-14/2023-03-26')
        .then((value) => {
            resourceLog.history = value.data
            generateChart()
        })
}

function generateChart() {
    data.value = {
        labels: resourceLog.history?.labels,
        datasets: [
            {
                label: 'CPU',
                backgroundColor: '#60a5fa',
                data: resourceLog.history?.resource_log_count.cpu,
            },
            {
                label: 'Memory',
                backgroundColor: '#4ade80',
                data: resourceLog.history?.resource_log_count.memory,
            },
            {
                label: 'hdd',
                backgroundColor: '#f87171',
                data: resourceLog.history?.resource_log_count.hard_disk,
            },
            {
                label: 'web_server',
                backgroundColor: '#34d399',
                data: resourceLog.history?.resource_log_count.network,
            },
            {
                label: 'network',
                backgroundColor: '#c084fc',
                data: resourceLog.history?.resource_log_count.web_server,
            },
        ],
    }
}

generateChart()

onMounted(() => {
    getResourceLogHistories()
})
</script>
