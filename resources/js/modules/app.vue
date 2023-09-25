<template>
    <div>
        <HeaderPartial />
        Welcome, {{ store.user.name }}!
        <div>{{ status }}</div>
        <button type="button" @click="updateStatus()">Change Status</button>
    </div>
</template>

<script>
    import { store } from './../store.js'
    import HeaderPartial from './components/HeaderPartial.vue'

    export default {
        data() {
            return {
                store,
                status: 'online',
            }
        },
        methods: {
            updateStatus() {
                if (this.status == 'online')
                    this.status = 'offline';
                else
                    this.status = 'online'
            },
        },
        created() {
            axios.get('/api/user').then((response) => {
                store.user = response.data;
            })
        },
        components: {
            HeaderPartial
        },
    }
</script>