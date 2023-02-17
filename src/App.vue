<template>
    <div class="flex flex-col h-full mx-1">
        <div class="flex flex-row grow">
            <div class="m-1 w-full flex flex-col">
                <h1>Barracuda Garbage</h1>
                <textarea v-model="inputBox"></textarea>
            </div>
            <div class="m-1 w-full flex flex-col">
                <h1>Descrambled</h1>
                <textarea
                    ref="garbageOutArea"
                    v-model="outputBox"
                    disabled
                ></textarea>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, watch } from "vue";

const urlRegex = /https:\/\/linkprotect\.cudasvc\.com\/[^\s]+/g;
const inputBox = ref("");
const outputBox = ref("");

watch(inputBox, (val) => {
    outputBox.value = val.replace(urlRegex, (match) => {
        const url = new URL(match);
        const params = new URLSearchParams(url.search);
        console.info(match, url, params);
        return params.get("a") || "";
    });
});
</script>

<style scoped>
textarea {
    width: 100%;
    height: 100%;
    box-sizing: border-box;
    resize: none;
}
</style>
