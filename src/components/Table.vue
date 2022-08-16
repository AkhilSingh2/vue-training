<template>
  <div class="container">
      <table>
          <thead>
              <tr>
                  <th>Country</th>
                  <th>Capital</th>
                  <th>Population</th>
              </tr>
          </thead>

          <tbody>
            <tr v-for="country in displayedCountries" :key="country.alpha2Code">
                <td> {{country.name}}</td>
                <td> {{country.capital}}</td>
                <td> {{country.population}}</td>

            </tr>
            </tbody>

      </table>
      <button @click="page--">Previous</button>
      <button v-for="pageNumber in pages.slice(page-1,page+5)" :key="pageNumber" @click="page = pageNumber">{{ pageNumber }}</button>
      <button @click="page++">Next</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return{
            countries: [],
            page: 1,
            perPage: 10,
            pages: [],
            numberOfPages: 10
        }
    },
    mounted() {
        axios
            .get('https://restcountries.com/v2/regionalbloc/eu')
            .then(response => {
                this.countries = response.data
                // console.log(this.countries)
                console.log(this.displayedCountries)
                this.setPages()
            }
            )
            .catch(error => (
                console.log(error)
            ));
    

            
    },
    computed: {
        displayedCountries(){
            return this.paginate(this.countries)
        }
    },
    // watch: {
    //     countries () {
    //         this.setPages()
    //     }
    // },
    methods: {
        paginate(countries) {
            let from = (this.page * this.perPage) - this.perPage
            let to = this.page * this.perPage
            return countries.slice(from, to)
        },
        setPages() {
            for(let index= 1; index <= this.numberOfPages; index ++) {
                this.pages.push(index)
            }
        }

    }
}
</script>

<style>

</style>