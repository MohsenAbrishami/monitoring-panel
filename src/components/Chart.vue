<template>
    <div class="w-9/12 bg-white my-5 mx-auto p-5 rounded-lg">
        <div class="w-2/12 inline-block float-left pt-10">
            <button class="w-32 bg-blue-400 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                CPU
            </button>
            <button class="w-32 bg-green-400 hover:bg-green-700 text-white font-bold py-2 px-4 rounded mt-3">
                Memory
            </button>
            <button class="w-32 bg-red-400 hover:bg-red-700 text-white font-bold py-2 px-4 rounded mt-3">
                HDD
            </button>
            <button class="w-32 bg-emerald-400 hover:bg-emerald-700 text-white font-bold py-2 px-4 rounded mt-3">
                Web Server
            </button>
            <button class="w-32 bg-purple-400 hover:bg-purple-700 text-white font-bold py-2 px-4 rounded mt-3">
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

const cpu = ref([40, 39, 10, 40, 39, 80, 40])
const memory = ref([10, 2, 40, 50, 30, 70, 40])
const hardDisk = ref([1, 20, 4, 5, 30, 7, 40])
const webServer = ref([5, 10, 30, 40, 20, 10, 40])
const network = ref([80, 2, 40, 50, 30, 7, 40])

const data = ref({
    labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
    datasets: [
        {
            label: 'CPU',
            backgroundColor: '#60a5fa',
            data: cpu,
        },
        {
            label: 'Memory',
            backgroundColor: '#4ade80',
            data: memory,
        },
        {
            label: 'hdd',
            backgroundColor: '#f87171',
            data: hardDisk,
        },
        {
            label: 'web_server',
            backgroundColor: '#34d399',
            data: webServer,
        },
        {
            label: 'network',
            backgroundColor: '#c084fc',
            data: network,
        },
    ],
})

const options = {
    responsive: true,
    maintainAspectRatio: false,
}

const resourceLog = reactive({
    history: null,
})

function getResourceLogHistories() {
    axios.get('http://localhost:8000/monitor/history/2020-01-01/2023-12-12')
        .then((value) => {
            resourceLog.history = value.data
            resourceLog.history[0].forEach((element) => {
                console.info(element.id)
            })
        })
}

onMounted(() => {
    getResourceLogHistories()
})
</script>
