<template>
    <nav
        class="navbar navbar-expand-lg"
        :class="[
            `navbar-${theme}`,
            `bg-${theme}`,
            'navbar',
            'navbar-expand-lg',
        ]"
    >
        <div class="container-fluid">
            <a class="navbar-brand" href="#">My Vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <li
                    class="nav-item"
                    v-for="(page, index) in publishedPages"
                    :key="index"
                >
                    <NavbarLink
                        :page="page"
                        :isActive="activePage === index"
                        @click.prevent="navLinkClick(index)"
                    ></NavbarLink>
                </li>
            </ul>
            <form class="d-flex">
                <button class="btn btn-primary" @click.prevent="changeTheme">
                    Change navbar(theme)
                </button>
            </form>
        </div>
    </nav>
</template>

<script>
import NavbarLink from "./NavbarLink.vue";
export default {
    components: {
        NavbarLink,
    },
    created() {
        this.getThemeSetting();
    },
    computed: {
        publishedPages() {
            return this.pages.filter((p) => p.published);
        },
    },
    props: ["pages", "activePage", "navLinkClick"],
    data() {
        return {
            theme: "light",
        }; 
    },
    methods: {
        changeTheme() {
            let theme = "light";
            if (this.theme == "light") {
                theme = "dark";
            }
            this.theme = theme;
            this.storeThemeSetting();
            this.$emit("themeChanged", this.theme == "dark" ? "dark" : "theme");
        },
        storeThemeSetting() {
            localStorage.setItem("theme", this.theme);
        },
        getThemeSetting() {
            let theme = localStorage.getItem("theme");
            if (theme) {
                this.theme = theme;
            }
        },
    },
 
};
</script>

<style></style>
