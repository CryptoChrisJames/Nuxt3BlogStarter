<template>
    <div>
        <div v-for="blog in data" :key="blog">
            <div @click="goToPost(blog._path)">
                <div>
                    <p>{{ blog.date }} <span>&nbsp;&nbsp;&nbsp;{{ blog.title }}</span></p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
const router = useRouter();
const { data } = useAsyncData('posts', 
    () => queryContent()
            .only(['title', '_path', 'description', 'date'])
            .sort({ date: -1 })
            .find());
const goToPost = (path) => {
    router.push(`post${path}`);
};
</script>