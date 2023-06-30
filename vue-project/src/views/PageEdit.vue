<template>
    <div class="container mb-3">
        <h1>Edit {{ page.pageTitle }}</h1>
        <form action="">
            <div class="d-flex gap-3">
                <div class="col-sm-8">
                    <div class="mb-3">
                        <label for="" class="form-label">Page Title</label>
                        <input
                            type="text"
                            class="form-control"
                            v-model="page.pageTitle"
                        />
                    </div>
                    <div class="mb-3">
                        <label for="" class="form-label">Content</label>
                        <textarea
                            type="text"
                            class="form-control"
                            rows="5"
                            v-model="page.content"
                        ></textarea>
                    </div>
                </div>
                <div class="col-sm-4">
                    <div class="mb-3">
                        <label for="" class="form-label">Link Text</label>
                        <input
                            type="text"
                            class="form-control"
                            v-model="page.link.text"
                        />
                    </div>
                    <div class="form-check">
                        <label class="form-check-label">
                            <input
                                type="checkbox"
                                class="form-check-input"
                                v-model="page.published"
                            />
                            published
                        </label>
                    </div>
                </div>
            </div>
            <div class="mb-3">
                <button class="btn btn-primary me-2" @click.prevent="submit">
                    Edit
                </button>
                <button 
                class="btn btn-secondary me-2"
                @click.prevent="goToPagesList"
                >Cancel</button>
                <button 
                class="btn btn-danger"
                @click.prevent="deletePage"
                >Delete</button>
            </div>
        </form>
    </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import { inject } from "vue";

const router = useRouter();
const pages = inject("$pages");
const bus = inject("$bus");

const { index } = defineProps(["index"]);

let page = pages.getSinglePage(index);

const submit = () => {
    pages.editPage(index, page);

    bus.$emit("page-updated", {
        index,
        page,
    });
    goToPagesList();
};
const deletePage = () => {
    pages.removePage(index)

    bus.$emit('page-deleted',{index} )
    goToPagesList()
}

const goToPagesList = () => {
    router.push({ path: "/pages" });
};
</script>
