<template>
    <div class="w-fit mx-auto mt-24 bg-white rounded-lg p-2">
        <span class="pl-3 font-bold inline-block">Monitoring Overview:</span>
        <a href="">
            <img src="public/refresh.png" class="w-10 inline-block float-right mr-3">
        </a>
        <div class="flex justify-center pt-10 pb-4">
            <div class="h-28 w-64 bg-red-100 ml-3 p-2 inline-block rounded-lg">
                <span>Cpu Usage</span>
                <div class="pt-4">
                    <span class="inline-block">10%</span>
                    <img
                        class="inline-block float-right"
                        src="public/cpu-icon.png"
                        width="50px"
                    >
                </div>
            </div>
            <div class="h-28 w-64 bg-green-100 ml-5 p-2 inline-block rounded-lg">
                <span>Memory Usage</span>
                <div class="pt-4">
                    <span class="inline-block">10%</span>
                    <img
                        class="inline-block float-right"
                        src="public/ram-icon.png"
                        width="50px"
                    >
                </div>
            </div>
            <div class="h-28 w-64 bg-green-100 ml-5 p-2 inline-block rounded-lg">
                <span>Hard Disk Free Space</span>
                <div class="pt-4">
                    <span class="inline-block">10%</span>
                    <img
                        class="inline-block float-right"
                        src="public/harddisk-icon.png"
                        width="50px"
                    >
                </div>
            </div>
            <div class="h-28 w-64 bg-red-100 ml-5 p-2 inline-block rounded-lg">
                <span>Web server status</span>
                <div class="pt-4">
                    <span class="inline-block">10%</span>
                    <img
                        class="inline-block float-right"
                        src="public/web-server-icon.png"
                        width="50px"
                    >
                </div>
            </div>
            <div class="h-28 w-64 bg-green-100 ml-5 mr-2 p-2 inline-block rounded-lg">
                <span>Network connection</span>
                <div class="pt-4">
                    <span class="inline-block">10%</span>
                    <img
                        class="inline-block float-right"
                        src="public/network-icon.png"
                        width="50px"
                    >
                </div>
            </div>
        </div>
    </div>
</template>
