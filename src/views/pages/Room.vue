<script>
import InputText from 'primevue/inputtext';
import Button from 'primevue/button';
import Card from 'primevue/card';
import io from 'socket.io-client';
import { ref, watch } from 'vue';
import { useRoute } from 'vue-router';

export default {
    data() {
        return {
            socket: {},
            msg: '',
            items: [],
            room: ''
        };
    },

    methods: {
        sendMsg() {
            if (this.msg !== '') {
                this.socket.emit('msg', this.msg);
                this.msg = '';
            }
        }
    },

    mounted() {
        // console.log(this.$route.params.room);
        const route = useRoute();
        this.room = ref(route.params.room);

        //connecting to server
        this.socket = io('http://localhost:8000');

        //joining room
        this.socket.emit('create', this.room);

        //getting msgs from server
        this.socket.on('reply', (msg) => {
            this.items.unshift({ message: msg });
        });
    }
};
</script>

<template>
    <div class="m-auto p-4 surface-hover h-screen">
        <h2 class="text-center">You are in: {{ room }}</h2>
        <div class="flex">
            <InputText v-model="msg" placeholder="Message..." class="flex-1" @keyup.enter="sendMsg()" />
            <Button label="Send" class="ml-2" @click="sendMsg()" />
        </div>
        <Card class="mt-4">
            <template #content>
                <div v-for="(item, index) in items" :key="item.id">
                    <p class="m-0">
                        {{ item.message }}
                    </p>
                    <hr v-if="index !== items.length - 1" :class="{ 'border-primary': index === 0 }" />
                </div>
            </template>
        </Card>
    </div>
</template>
