<template>
  <div class="home">
    <b-button-group>
      <b-dropdown right text="Sort by">
        <b-dropdown-item>Latest picture</b-dropdown-item>
        <b-dropdown-item>Oldest picture</b-dropdown-item>
        <b-dropdown-item>Popular picture</b-dropdown-item>
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
  {{ tenRecords }}
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Record from '../components/Record.vue';

@Component({
  components: {
    Record
  }
})
export default class Home extends Vue {
  key = "6phQ10lhL66iIFs4PyrwHR4PSl725CuHON0BFPpQ1g0";
  tenRecords: any = [];

  mounted(){
    this.getTenRecords;
  }
  async getTenRecords(){
    const response = await fetch(`https://api.unsplash.com/search/photos?&query=skyscraper&client_id=${ this.key }`);
    console.log(response);
    const json = await response.json();
    console.log(response);
    this.tenRecords = json.results;
    console.log(json.results);
  }

  // order(): void{
  //   this.tenRecords.sort(function(a: any, b: any) {
  //     return b.likes - a.likes;
  //   });
  // }
}
</script>