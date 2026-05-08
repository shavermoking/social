<script>
export default {
    name: "App",
    data() {
        return {
            token: null
        }
    },

    mounted() {
        this.getToken()
    },

    watch: {
        $route() {
            this.getToken()
        }
    },

    methods: {
        getToken() {
            this.token = localStorage.getItem('x_xsrf_token')
        },

        logout() {
            axios.post('/logout')
                .then(res => {
                    localStorage.removeItem('x_xsrf_token')
                    this.token = null
                    this.$router.push({name: 'user.login'})
                })
        }
    }
}
</script>

<template>
    <div class="w-96 mx-auto"> Personal</div>
</template>

<style scoped>
</style>
