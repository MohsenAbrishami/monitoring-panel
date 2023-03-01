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
    axios.get('http://localhost:8000/monitor/history/2020-01-01/2023-12-12')
        .then((value) => {
            resourceLog.history = value.data
            resourceLog.history[0].forEach((element) => {
                console.info(element.id)
            })
        })
}

function generateChart() {
    data.value = {
        labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
        datasets: [
            {
                label: 'CPU',
                backgroundColor: '#60a5fa',
                data: randomList(),
            },
            {
                label: 'Memory',
                backgroundColor: '#4ade80',
                data: randomList(),
            },
            {
                label: 'hdd',
                backgroundColor: '#f87171',
                data: randomList(),
            },
            {
                label: 'web_server',
                backgroundColor: '#34d399',
                data: randomList(),
            },
            {
                label: 'network',
                backgroundColor: '#c084fc',
                data: randomList(),
            },
        ],
    }
}

function randomList() {
    const newArray = []

    for (let i = 0; i < 10; i++) {
        const randomValue = Math.floor(Math.random() * 10)
        newArray.push(randomValue)
    }

    return newArray
}

generateChart()

onMounted(() => {
    getResourceLogHistories()
})
</script>
