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
    <div class="w-96 mx-auto">
        <div>
            <div>
                <input v-model="title" class="w-96 mb-3 rounded-3xl border p-2  border-slate-400" type="text" placeholder="title">
            </div>
            <div>
                <textarea v-model="content" class="w-96 mb-3 rounded-3xl border p-2  border-slate-400" placeholder="content" type="text"></textarea>
            </div>
            <div>
                <a href="#" class="block w-32 text-center rounded-3xl bg-green-600 text-white
                 hover:bg-white hover:border hover:border-green-600 hover:text-green-600 hover:box-content">Publish</a>
            </div>
        </div>

    </div>
</template>

<style scoped>
</style>
