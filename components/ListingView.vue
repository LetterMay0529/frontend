<template>
    <div>
        <button class="btn btn-success float-right" @click="onNew">
            New Listing
        </button>
        <h5>Listing View</h5>
        <hr>

        <form action="" @submit.prevent="onSave">

            <b-form-group label="Property Type" label-for="prop_type">
                <b-form-select v-model="listing.prop_type" :options="types"></b-form-select>
            </b-form-group>

            <b-form-group label="Property Category" label-for="prop_category">
                <b-form-select v-model="listing.prop_category" :options="categories"></b-form-select>
            </b-form-group>

            <b-form-group label="Location">
                <b-form-input v-model="listing.location"></b-form-input>
            </b-form-group>
            
            <b-form-group label="Value">
                <b-form-input v-model="listing.value"></b-form-input>
            </b-form-group>

            <b-form-group label="Description">
                <b-form-input v-model="listing.description"></b-form-input>
            </b-form-group>

            <b-form-group label="Acquired On">
                <b-form-input type="date" v-model="listing.acquired_on"></b-form-input>
            </b-form-group>
            <b-form-group>
                <button class="btn btn-primary" type="submit">Save Changes</button>
                <button class="btn btn-danger float-right" type="button" @click="onDelete" v-if="listing.id">Delete Item</button>
            </b-form-group>
        </form>
    </div>
</template>

<script>
export default {
    props:{
        listing: {},
    },
    
    data() {
        return {
            types: [
                {value: 'For Rent', text: 'For Rent'},
                {value: 'For Sale', text: 'For Sale'},
                {value: 'Foreclosure', text: 'Foreclosure'},
            ],

            categories: [
                {value: 'Land', text: 'Land'},
                {value: 'Commercial', text: 'Commercial'},
                {value: 'Residential', text: 'Residential'},
            ],
        }
    },
    methods: {
        async onSave() {
            try {
                if(!this.listing.id) {
                    await this.$axios.post('/api/listings', this.listing)
                }else{
                    await this.$axios.put('/api/listings/' + this.listing.id, this.listing)
                }
                this.$emit('saved')
            } catch (err) {
                alert(err.response.data.message)
            }
        },
        onNew() {
            this.$emit('newListing')
        },
        async onDelete() {
            try {
                this.$axios.delete('/api/listings/' + this.listing.id)
                this.$emit('deleted')
            } catch (err) {
                alert(err.response.data.message)
            }
        }
    }
}
</script>