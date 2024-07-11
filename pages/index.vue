<template>
    <div class="flex flex-col gap-3">
        <div class="flex flex-row gap-3">
            <button type="button" class="bg-gray-200 p-3" @click="startRecorder">Start</button>
            <button type="button" class="bg-gray-200 p-3" @click="">Stop</button>
        </div>
        </div class="flex flex-row gap-3">
            <input type="text" v-model="form.www" />
        <div>
    </div>
</template>

<script lang="js" setup>
import { chromium } from 'playwright';

const form = reactive({
    www: 'about:blank',
});

const startRecorder = async () => {
    let browser = await chromium.launch({ headless: false });
    const context = await browser.newContext();
    let currentPage = await context.newPage();
    let client = await currentPage.context().newCDPSession(currentPage);
    await client.send('Page.startScreencast', { format: 'jpeg', quality: 75 });
};
</script>