<template>
    <div>
        <h1>this is the random page</h1>
        <RandomRecord
        v-if='randomRecord.urls'
        :randomData="randomRecord"/>
        <button @click="getRandome">Another random</button>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import RandomRecord from '../components/RandomRecord.vue';

@Component({
    components:{
        RandomRecord
    }
})
export default class Random extends Vue {
    key = "6phQ10lhL66iIFs4PyrwHR4PSl725CuHON0BFPpQ1g0";
    randomRecord = {};

    mounted() {
        this.getRandome();
    }

    async getRandome(){
        const response = await fetch(`https://api.unsplash.com/photos/random?query=skyscraper&client_id=${ this.key }`);
        const json = await response.json();
        this.randomRecord = json;
    }
}
</script>