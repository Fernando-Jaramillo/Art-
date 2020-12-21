<template>
    <div>
        <b-col>
            <b-card
            title=" "
            :img-src="pic.urls.small"
            img-alt="Image"
            img-top
            style="max-width: 30rem;"
            class="mb-2 mt-5"
            >
            <b-card-title> Title </b-card-title>
            <b-card-text> Year </b-card-text>
            <b-button to="/details" @click="sendData" variant="primary">Details</b-button>
            </b-card>
        </b-col>
    </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";
import { bus } from '../main';

@Component
export default class Record extends Vue {
    @Prop() private pic!: any ;
    
    picId = {};

    created(){
        this.picId = this.pic.id; 
    }

    sendData(){
        bus.$emit('passData', this.picId);
    }
}
</script>