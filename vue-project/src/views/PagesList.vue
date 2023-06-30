<template>
    <div>
        <!-- <p>{{ data.counter }}</p>

        <button @click.prevent="data.counter++">+</button> -->
        <h1>Pages</h1>
        <div class="text-end">
            <router-link to="/pages/create" class="btn btn-primary"
                >New Page</router-link
            >
        </div>
        <table class="table table-hover">
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Link Text</th>
                    <th>Is Published</th>
                </tr>
            </thead>
            <tbody>
                <tr 
                v-for="(page, index) in $pages.getAllPages()" 
                :key="index"
                @click="goToPage(index)"
                >
                    <td>{{ page.pageTitle }}</td>
                    <td>{{ page.link.text }}</td>
                    <td>{{ page.published ? "yes" : "no" }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
import { 
    // ref, reactive, 
    inject } from "vue";
import { useRouter } from "vue-router";

// const counter = ref(0) //{value:0}
// const data = reactive({ counter: 0 });
const $pages = inject("$pages");
const router = useRouter()

function goToPage(index){
    router.push({path:`pages/${index}/edit`})
}
// const click = () => {
//     // counter.value++
//     data.counter++
// }
</script>

<!-- <script>
export default {
    data(){
        return{
            counter:0
        }
    },
    methods:{
        click(){
            this.counter++
        }
    }
}
</script> -->
<style scoped>
.table.table-hover tr:hover{
    cursor: pointer;
}
</style>