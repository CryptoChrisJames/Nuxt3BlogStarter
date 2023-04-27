<template>
    <div v-if="currentBlog" >
        <h2>{{ currentBlog.title }}</h2>
        <p>{{ currentBlog.date }}</p>
        <p>{{ currentBlog.description }}</p>
        <ContentRenderer>
            <ContentRendererMarkdown :value="currentBlog" />
        </ContentRenderer>
    </div>
</template>

<script setup>
const { post } = useRoute().params;
const { data } = useAsyncData('post', 
    () => queryContent().where({_path: `/${post}`}).findOne());
var currentBlog = data;
</script>