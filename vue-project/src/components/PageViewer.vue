<template>
    <div class="container" :class="[theme == 'dark' && 'text-warning']">
        <h1 class="emphasize" :class="[theme == 'dark' && 'text-warning']">
            {{ page.pageTitle }}
        </h1>
        <p>{{ page.content }}</p>
    </div>
</template>

<script>
export default {
    props: {
        page: {
            type: Object,
            default(rawProps) {
                return {
                    pageTitle: "",
                    content: "",
                };
            },
        },
        theme: {
            type: String,
        },
    },
};
</script>

<style scoped>
.emphasize {
    color: blue;
}
</style>
