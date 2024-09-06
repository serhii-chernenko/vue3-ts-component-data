<script setup lang="ts">
import { ref, computed } from 'vue'

interface Post {}

// you should explicitly type this 👇
const posts = ref([])

// try explicitly typing this too
// (even though it's not strictly necessary) 👇
const numberOfPosts = computed(() => posts.value.length)

async function loadPosts() {
    const res = await fetch('/api.json')
    posts.value = await res.json()
}

loadPosts()
</script>
<template>
    <div class="page">
        <div>
            <h1>Posts ({{ numberOfPosts }})</h1>
            <ul>
                <li v-for="(post) in posts" :key="(post as any).id">
                    {{ (post as any).title }}
                </li>
            </ul>
        </div>
    </div>
</template>
