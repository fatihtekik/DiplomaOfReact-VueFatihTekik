<script>
export default {
    name: "MapItems",
    props: {
        width: { type: String },
        border: { type: String, required: true },
        background: { type: String, required: true },
        color: { type: String, required: true },
    },
    data() {
        return {
            buddies: [],
        }
    },
    methods: {
        async fetchBuddies() {
            try {
                const response = await this.$axios.get('https://valorant-api.com/v1/maps');
                this.buddies = response.data.data;
                console.log(response.data.data);
            } catch (error) {
                console.error('Ошибка', error);
            }
        },
    },
    mounted() {
        this.fetchBuddies();
    },
}
</script>

<template>
    <div class="back">
        <a href="/content"><img src="https://icones.pro/wp-content/uploads/2021/06/symbole-fleche-gauche-bleu.png" class="link-back" alt=""></a>
    </div>
    <section class="map-items">
        <div class="map-item" v-for="buddy in buddies.splice(0,21)" :key="buddy.uuid">
            <img class="map-item_img" :src="buddy.splash" alt="">
            <p class="map-item_title"> {{ buddy.displayName }}</p>
        </div>
    </section>
</template>

<style scoped>

.back{
    width: 1169px;
    margin: 0 auto;
}
.link-back{
    width: 148px;
    height: 148px;
    margin: 0 auto;

}
.map-items {
    padding-top: 20px;
    width: 1169px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(5, 1fr);
    grid-column-gap: 0px;
    grid-row-gap: 0px;

}

.map-item {
    transition: 1s;
    text-align: center;
}

.map-item:hover {
    transform: scale(1.1);
}

.map-title {
    font-size: 146px;
    color: #0e3eff;
    font-family: 'Montserrat', sans-serif;
}

.map-item_img {
    height: 300px;
    width: 300px;
}

.map-item_title {
    color: #0e3eff;
    font-family: 'Montserrat', sans-serif;
    font-size: 26px;
}
@media only screen and (max-width: 768px) {
    .map-items {
    padding-top: 20px;
    width: 768px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(2 , 1fr);
    grid-template-rows: repeat(5, 1fr);
    grid-column-gap: 0px;
    grid-row-gap: 0px;

}
}

@media only screen and (max-width: 320px) {
    .map-items {
    padding-top: 20px;
    width: 320px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    grid-template-rows: repeat(5, 1fr);
    grid-column-gap: 0px;
    grid-row-gap: 0px;

}
}
</style>