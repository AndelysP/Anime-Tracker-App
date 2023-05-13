<template>
    <div class="card">
        <img :src="anime.images.jpg.large_image_url" :alt="anime.title + ' Poster'" @click="showModal = true"
            class="card-img" />
        <h3>{{ anime.title }}</h3>

        <!-- Modal -->
        <div v-if="showModal" class="modal">
            <div class="modal-content">
                <div class="content">
                    <div class="left-content">
                        <h2>{{ anime.title }}</h2>
                        <img :src="anime.images.jpg.large_image_url" :alt="anime.title + ' Poster'" class="modal-img" />
                    </div>

                    <div class="right-content">
                        <ul>
                            <li v-for="genre in anime.genres" :key="genre.mal_id" :class="getGenreClass(genre.name)">
                                <p class="genre">{{ genre.name }}</p>
                            </li>
                        </ul>
                        <p>{{ anime.synopsis }}</p>
                        <p>Nombre d'épisodes vus: {{ episodesWatched }} / {{ anime.episodes }}</p>
                        <button @click="incrementEpisodes" class="btn-increment">Ajouter un épisode</button>
                        <button @click="decrementEpisodes" class="btn-decrement">Supprimer un épisode</button>
                    </div>
                </div>

                <span class="close" @click="showModal = false">&times;</span>
            </div>

        </div>
    </div>
</template>

<script>
export default {
    props: ['anime'],
    data() {
        return {
            showModal: false,
            localStorageKey: `episodesWatched_${this.anime.title.replace(/[^a-z0-9]/gi, '_')}`,
            episodesWatched: 0
        };
    },
    mounted() {
        const savedEpisodesWatched = localStorage.getItem(this.localStorageKey);
        if (savedEpisodesWatched) {
            this.episodesWatched = parseInt(savedEpisodesWatched);
        }
    },
    watch: {
        episodesWatched(newEpisodesWatched) {
            localStorage.setItem(this.localStorageKey, newEpisodesWatched.toString());
        }
    },
    methods: {
        incrementEpisodes() {
            if (this.episodesWatched < this.anime.episodes) {
                this.episodesWatched++;
            }
        },
        decrementEpisodes() {
            if (this.episodesWatched > 0) {
                this.episodesWatched--;
            }
        },
        getGenreClass(genreName) {
            const genreClassMap = {
                Action: 'genre-action',
                Adventure: 'genre-adventure',
                Fantasy: 'genre-fantasy',
                Comedy: 'genre-comedy',
                Horror: 'genre-horror',
                Supernatural: 'genre-supernatural',
                Mystery: 'genre-mystery',
                Sports: 'genre-sports',
                Drama: 'genre-drama'
            };
            return genreClassMap[genreName] || 'genre-default';
        }
    }
};
</script>
