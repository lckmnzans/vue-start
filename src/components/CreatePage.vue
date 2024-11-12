<template>
    <div class="container mb-3">
        <form action="">
            <div class="mb-3">
                <label for="" class="form-label">Page Title</label>
                <input type="text" class="form-control" :value="pageTitle" @input="(e) => pageTitle = e.target.value">
            </div>
            <div class="mb-3">
                <label for="" class="form-label">Content</label>
                <textarea type="text" class="form-control" v-model="content" rows="5"></textarea>
            </div>
            <div class="mb-3">
                <label for="" class="form-label">Link Text</label>
                <input type="text" class="form-control" v-model="linktext"></input>
            </div>
            <div class="mb-3">
                <label for="" class="form-label">Link URL</label>
                <input type="text" class="form-control"  v-model="linkurl"></input>
            </div>
            <div class="row mb-3">
                <div class="form-check">
                    <input type="checkbox" class="form-check-input">
                    <label for="gridCheck1" class="form-check-label">Published</label>
                </div>
            </div>

            <div class="mb-3">
                <button class="btn btn-primary" :disabled="isFormInvalid" @click.prevent="submitForm">Create Page</button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    props: ['pageCreated'],
    computed: {
        isFormInvalid() {
            return (!this.pageTitle || !this.content || !this.linktext || !this.linkurl);
        }
    },
    data() {
        return {
            pageTitle: '',
            content: '',
            linktext: '',
            linkurl: ''
        }
    },
    methods: {
        submitForm() {
            if (!this.pageTitle || !this.content || !this.linktext || !this.linkurl) {
                alert('Please fill all forms');
                return;
            }

            this.pageCreated({
                pageTitle: this.pageTitle,
                content: this.content,
                link: {
                    linktext: this.linktext,
                    linkurl: this.linkurl
                }
            })
        }
    }
}
</script>