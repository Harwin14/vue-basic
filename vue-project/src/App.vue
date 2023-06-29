<template>
    <div
        class="vh-100"
        :class="[
            { 'bg-dark': theme === 'dark', 'text-light': theme === 'dark' },
        ]"
    >
        <!-- <navbar
            :pages="pages"
            :active-page="activePage"
            :nav-link-click="(index) => (activePage = index)"
            @theme-changed="handleTheme"
            @get-theme="getTheme"
        ></navbar> -->
        <navbar></navbar>
        <router-view></router-view>
        <!-- <page-viewer
            v-if="pages.length > 0"
            :page="pages[activePage]"
            :theme="theme"
        />
        <create-page @page-created="pageCreated" /> -->
    </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import PageViewer from "./components/PageViewer.vue";
import CreatePage from "./components/CreatePage.vue";


export default {
    components: {
        Navbar,
        PageViewer,
        CreatePage,
    },
    // created() {
    //     this.getPages();
    //     this.getThemeSetting();
    // },
    // data() {
    //     return {
    //         theme: "light",
    //         activePage: 0,
    //         pages: [],
    //     };
    // },
    methods: {
        // async getPages() {
        //     let res = await fetch("pages.json");
        //     let data = await res.json();
        //     this.pages = data;
        // },
        // handleTheme(theme) {
        //     this.theme = theme;
        // },
        // getThemeSetting() {
        //     let theme = localStorage.getItem("theme");
        //     if (theme) {
        //         this.theme = theme;
        //     }
        // },
        pageCreated(pageobj) {
            this.pages.push(pageobj);
        },
    },
};
</script>

<style></style>
