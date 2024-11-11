<template>
<nav :class="[`navbar-${theme}`,`bg-${theme}`, 'navbar', 'navbar-expand-lg']">
    <div class="container-fluid">
        <a class="navbar-brand" href="#">MyVue</a>
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li  v-for="(page, index) in pages" class="nav-item" :key="index">
                <navbar-link :page="page" :is-active="activePage == index" @click.prevent="navLinkClick(index)"></navbar-link>
            </li>
        </ul>
        <form class="d-flex">
            <button class="btn btn-primary"
            @click.prevent="changeTheme();storeThemeSetting()"
            >Toggle NavBar</button>
        </form>
    </div>
</nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue';
export default {
    props:['pages','activePage','navLinkClick'],
    components:{
        NavbarLink
    },
    created() {
        this.getThemeSetting();
    },
    data() {
        return {
            theme: 'light'
        }
    },
    methods: {
        changeTheme() {
            let theme = 'light';

            if (this.theme == 'light') {
                theme = 'dark';
            }
            this.theme = theme;
        },
        storeThemeSetting() {
            localStorage.setItem('theme', this.theme);
        },
        getThemeSetting() {
            let theme = localStorage.getItem('theme');

            if (theme) {
                this.theme = theme;
            }
        }
    }
}
</script>