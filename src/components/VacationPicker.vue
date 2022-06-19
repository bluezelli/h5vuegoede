<template>
    <div>
        <h1>{{ header }}</h1>
        <div class="row">
            <div class="col-6">
               
                <input type="text" class="form-control-lg"
                       v-model="filterText">
                <ul class="list-group">
                    <li class="list-group-item"
                        @click="selectCountry(index)"
                        v-for="(country, index) in countryList(filterText)"
                        v-bind:key="country.id">
                        <span v-bind:id="country.id"
                              v-bind:title="country.details">
                              {{ country.id }} 
                              {{country.name}}
                        </span>
                    </li>
                </ul>
                <hr>
                <h2>GoedKope plekken</h2>
                <select class="form-control-lg"
                        v-model="selectedCost"
                        @change="filterCountries()">
                    <option v-for="(cost, index) in costs"
                            :key="index"
                            :value="cost">
                        {{ cost }}
                    </option>
                </select>
                <ul class="list-group">
                    <li v-for="(country, index) in filteredCountries"
                        :key="index"
                        class="list-group-item">
                        {{ country.name }} {{country.cost}}
                    </li>
                </ul>
            </div>
            <div class="col-6">
                <h2>Selected:</h2>
                <ul class="list-group">
                    <li class="list-group-item">{{ selectedCountry.id}}</li>
                    <li class="list-group-item">{{ selectedCountry.name}}</li>
                    <li class="list-group-item">{{ selectedCountry.capital}}</li>
                    <!-- <li class="list-group-item">
                        <img :src="getImgUrl(selectedCountry.img)"
                             :alt="selectedCountry.img"
                             class="img-fluid">
                    </li> -->
                    <li class="list-group-item">{{ selectedCountry.details}}</li>
                    <li class="list-group-item" v-if="isExpensive">
                        <span class="badge badge-danger badge-pill">Expensive!</span>
                    </li>
                    <li class="list-group-item" v-if="isOnSale">
                        <span class="badge badge-warning badge-pill">On Sale!</span>
                    </li>
                </ul>
            </div>
        </div>
    </div>

</template>

<script>
    import countryData from '@/countryData';


    export default {
        name: "VacationPicker",
        
        data() {
            return {
                countryData,
                header: 'vakantie picker',
                selectedCountryIndex: 0,
                selectedCost: 1000,
                costs: [1000, 2000, 3000, 4000, 5000, 6000],
                filteredCountries: [],
                filterText: ''
            }
        },
        methods: {
            // getImgUrl(img){
            //     return require('../assets/img' + img)
            // },
            selectCountry(index) {
                this.selectedCountryIndex = index;
            },
            filterCountries() {
                
                console.log(this.selectedCost);
                this.filteredCountries = this.countryData.countries.filter(country => country.cost < this.selectedCost)
            },
            countryList(filterText) {
                if (!filterText) {
                    return this.countryData.countries;
                }
                return this.countryData.countries.filter(country => {
                    return country.name
                });
            }
        },
        computed: {
            selectedCountry() {
                return {
                    ...this.countryData.countries[this.selectedCountryIndex]
                }
            },
            isExpensive() {
                return countryData.countries[this.selectedCountryIndex].cost > 4000;
            },

            isOnSale() {
                return countryData.countries[this.selectedCountryIndex].cost < 1000;
            }
        }
    }
</script>