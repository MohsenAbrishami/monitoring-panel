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
import { onMounted } from 'vue'
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

const data = {
    labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
    datasets: [
        {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: [40, 39, 10, 40, 39, 80, 40],
        },
    ],
}

const options = {
    responsive: true,
    maintainAspectRatio: false,
}

onMounted(() => {
    getCurrentStatus()
})

function getCurrentStatus() {
    axios.get('http://localhost:8000/api/monitor/current')
        .then((value) => {
            console.log(value)
        }).catch(() => {
            alert('fail')
        })
}

</script>

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
