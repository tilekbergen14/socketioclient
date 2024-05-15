<script>
export default {
    data() {
        return {
            room: ''
        };
    },

    methods: {
        joinRoom() {
            if (this.room !== '') {
                // console.log(this.room);
                this.$router.push(`/room/${this.room}`);
                this.room = '';
            }
        }
    },

    mounted() {}
};
</script>

<template>
    <div class="m-auto p-4 surface-hover h-screen text-center flex justify-content-center align-content-center">
        <div class="lg:w-4 flex flex-column justify-content-center">
            <h1>Chat application using Socket.IO</h1>
            <Card class="mt-4">
                <template #content>
                    <InputText v-model="room" placeholder="Join room..." class="w-full flex-1 h-4rem" />
                    <br />
                    <Button label="Join" class="mt-3 w-full" @click="joinRoom" />
                </template>
            </Card>
        </div>
    </div>
</template>
