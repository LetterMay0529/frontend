<template>
    <div>
        <NavBar />
        <div class="container">
            <div class="row">
                <div class="col-6">
                    <h5>Listings</h5>
                    <hr>
                    <ul class="list-group">
                        <li class="list-group-item list-group-item-action"  v-for="listing in listings" :key="listing.id" @click="onSelected(listing)">
                            {{listing.prop_type}} <span class="float-right">{{listing.value}}</span>
                        </li>
                    </ul>
                </div>
                <div class="col-4">
                    <ListingView :listing="selectedListing" @saved="onChange" @newItem="onNew" @deleted="onChange" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            listings: [],
            selectedListing: {}
        }
    },
    methods: {
        async getAllListing() {
            await this.$axios.get('/api/listings')
            .then((res)=>{
                if(res.status==200) {
                    this.listings = res.data
                }
            })
        },
        onChange() {
            this.getAllListing()
            this.selectedListing = {}
        },
        onSelected(listing) {
            this.selectedListing = listing;
        },
        onNew() {
            this.selectedListing = {}
        },
    },
    created() {
        this.getAllListing()
    }
}
</script>

