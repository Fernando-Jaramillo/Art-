<template>
    <div>
          <b-col>
            <b-card
            v-if="itemDetails.urls"
            title=" "
            :img-src="itemDetails.urls.small"
            img-alt="Image"
            img-top
            style="max-width: 30rem;"
            class="mb-2 mt-5"
            >
            <b-card-title> Author: {{ itemDetails.user.name }} </b-card-title>
            <b-card-text> Description: {{ itemDetails.description }} </b-card-text>
            </b-card>
        </b-col>
    </div>
</template>

<script lang='ts'>
import { Component, Prop, Vue } from 'vue-property-decorator';
import { bus } from '../main';

@Component
export default class Details extends Vue{
    key = "6phQ10lhL66iIFs4PyrwHR4PSl725CuHON0BFPpQ1g0";
    itemDetails = {};

    mounted(){
      this.getData();
    }

     getData(){
          //the function of looking for by ID of the API does not work. This is an alternative
         bus.$on('passData', (id: any) => {
          fetch(`https://api.unsplash.com/search/photos?&query=${ this.query }&client_id=${ this.key }`)
            .then((res) => {
                return res.json();
            })
            .then((ans) =>{
                const item = ans.results.find((item: any) => item.id == id)
                this.itemDetails = item;
            })
        })
    }
}
</script>