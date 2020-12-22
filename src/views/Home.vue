<template>
  <div class="home">
    <b-button-group>
      <b-dropdown right text="Sort by">
        <b-dropdown-item @click="orderByPopular">Popular picture</b-dropdown-item>
        <b-dropdown-item @click="orderBylargest">big to samll picture</b-dropdown-item>
        <b-dropdown-item @click="orderBySmallest">Small to big picture</b-dropdown-item>
      </b-dropdown>
    </b-button-group>
    <b-container>
      <b-card-group>
        <b-row cols="1" cols-sm="2" cols-md="3" cols-lg="5">
    <Record
      v-for="record in tenRecords"
      :key='record.id'
      :pic = "record"
      />
        </b-row>
      </b-card-group>
  </b-container>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Record from '../components/Record.vue';

@Component({
    components:{
        Record
    }
})
export default class Home extends Vue {
    key = "6phQ10lhL66iIFs4PyrwHR4PSl725CuHON0BFPpQ1g0";
    tenRecords = [];

    mounted() {
        this.getTenRecords();
    }

    orderByPopular() {
      this.tenRecords.sort((a: any, b: any) => a.likes - b.likes).reverse();
    }

    orderBySmallest(){
      this.tenRecords.sort(function(a: any, b: any) {
        return (a.width*a.height) - (b.width*b.height)
      });
      console.log(this.tenRecords);
    }
    async getTenRecords(){
        const response = await fetch(`https://api.unsplash.com/search/photos?&query=skyscraper&client_id=${ this.key }`);
        const json = await response.json();
        this.tenRecords = json.results;
        console.log(this.tenRecords);
    }
}
</script>