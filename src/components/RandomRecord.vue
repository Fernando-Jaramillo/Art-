<template>
    <div>
        <b-col>
            <b-card
            title=" "
            :img-src="randomData.urls.small"
            img-alt="Image"
            img-top
            style="max-width: 30rem;"
            class="mb-2 mt-5"
            >
            <b-card-title> Title </b-card-title>
            <b-card-text> Year </b-card-text>
            </b-card>
        </b-col>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue} from 'vue-property-decorator';

@Component
export default class RandomRecord extends Vue{
    @Prop() private randomData!: any;
}
</script>