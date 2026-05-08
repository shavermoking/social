<script>
export default {
    name: "Personal",
    data() {
        return {
            title: '',
            content: '',
            image: null,
        }
    },

    methods: {
        selectFile() {
            this.fileInput = this.$refs.file;
            this.fileInput.click();
        },
        storeImage(e) {
            const file = e.target.files[0]
            const formData = new FormData()
            formData.append('image', file)

            axios.post('/api/post_image', formData)
                .then( res => {
                    this.image = res.data.data
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
            <div class="flex mb-3 items-center">
                <div>
                    <input @change="storeImage" ref="file" type="file" class="hidden">
                    <a href="#" class="block mb-3 w-32 text-center rounded-3xl bg-green-600 text-white
                 hover:bg-white hover:border hover:border-green-600 hover:text-green-600 hover:box-content" @click.prevent="selectFile()">
                        Image
                    </a>
                </div>
            <div>
                <a @click.prevent="image = null" href="#" class="ml-3">Cancel</a>
            </div>
            </div>
            <div v-if="image">
                <img :src="image.url" alt="preview">
            </div>
            <div>
                <a href="#" class="block w-32 text-center rounded-3xl bg-green-600 text-white
                hover:bg-white hover:border hover:border-green-600 hover:text-green-600 hover:box-content ml-auto">
                    Publish
                </a>
            </div>
        </div>

    </div>
</template>

<style scoped>
</style>
