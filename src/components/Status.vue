<template>
    <div class="w-9/12 mx-auto mt-8 bg-white rounded-lg p-2">
        <span class="pl-3 pt-2 font-bold inline-block">Monitoring Overview:</span>
        <a href="">
            <img src="public/refresh.png" class="w-10 inline-block float-right mr-3">
        </a>
        <div class="w-full flex justify-center py-5">
            <div class="h-28 w-2/12 bg-red-100 p-2  rounded-lg">
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
            <div class="h-28 w-2/12 bg-green-100 ml-4 p-2 rounded-lg">
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
            <div class="h-28 w-2/12 bg-green-100 ml-4 p-2 rounded-lg">
                <span>Hard Disk Space</span>
                <div class="pt-4">
                    <span class="inline-block">10%</span>
                    <img
                        class="inline-block float-right"
                        src="public/harddisk-icon.png"
                        width="50px"
                    >
                </div>
            </div>
            <div class="h-28 w-2/12 bg-red-100 ml-4 p-2 rounded-lg">
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
            <div class="h-28 w-2/12 bg-green-100 ml-4 mr-2 p-2 rounded-lg">
                <span>Network Status</span>
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
