<template>
    <div>
        <router-link :to="{ name: 'get.index' }">Get </router-link>
        <router-link v-if="!token" :to="{ name: 'user.login' }">Login </router-link>
        <router-link v-if="token" :to="{ name: 'user.personal' }">Personal </router-link>
        <router-link v-if="!token" :to="{ name: 'user.registration' }">Registration </router-link>
        <a v-if="token" @click.prevent="Logout" href="#">Logout</a>
        <router-view :key="$route.fullPath"></router-view>
    </div>
</template>

<script>
export default {
    name: "Index",

    data() {
        return {
            token: null
        }
    },

    mounted() {
        this.getToken()
    },

    updated() {
        this.getToken()
    },

    methods: {
        getToken() {
            this.token = localStorage.getItem('x_xsrf_token')
        },

        Logout() {
            axios.post('/logout')
                .then( res => {
                    localStorage.removeItem('x_xsrf_token');
                    this.$router.push({ name: 'user.login'})
                })
        }
    }
}
</script>

<style scoped>

</style>
