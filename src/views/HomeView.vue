<script setup>
import InputText from 'primevue/inputtext';
import Button from 'primevue/button';
</script>

<template>
    <div class="flex flex-column m-4 align-center text-center">
        <h2>Simple chat application with Socket.IO</h2>
        <div><InputText v-model="msg" placeholder="Room..." class="flex-1" @keyup.enter="sendMsg()" /> <Button label="Join" class="ml-2" @click="sendMsg()" /></div>
    </div>
</template>
