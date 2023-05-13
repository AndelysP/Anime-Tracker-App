<template>
    <div class="card">
        <a :href="anime.url" target="_blank">
            <img :src="anime.images.jpg.image_url" :alt="anime.title + ' Poster'" >
        </a>
        <h3>{{ anime.title }}</h3>
    </div>
</template>

<script>
export default {
    props: ['anime']
}
</script>