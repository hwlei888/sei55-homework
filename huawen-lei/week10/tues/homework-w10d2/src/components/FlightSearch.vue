<template>
    <div>
        <h2>Search for Flights</h2>

        
        <label>Origin:
            <select v-model="origin" v-on:change="validate">
                <option value="">Please select:</option>
                <option value="SYD">Sydney</option>
                <option value="MEL">Melbourne</option>
                <option value="SIN">Singapore</option>
                <option value="SFO">San Francisco</option>
            </select>
        </label>
        
        <label>Destination:
            <select v-model="destination" @change="validate">
                <option value="">Please select:</option>
                <option value="SYD">Sydney</option>
                <option value="MEL">Melbourne</option>
                <option value="SIN">Singapore</option>
                <option value="SFO">San Francisco</option>
            </select>
        </label>
        <br>
        
        <div v-if="formErrorMessage.length > 0" class="error">{{formErrorMessage}}</div>

        <!-- <button v-on:click="submitSearch">Search Flights</button> -->
        <button @click="submitSearch">Search Flights</button>

        <p>Origin: {{origin}}</p>
        <p>Destination: {{destination}}</p>

    </div>
</template>

<script>
    export default {
      name: 'FlightSearch',
    
      data(){
        // This is the 'state' of our component; form values etc
        // need to be stored here
        return {
          origin: '',
          destination: '',
          formErrorMessage: '',
        };
      }, // data()
    
      methods: {
        submitSearch(){    // shorthand for submitSearch: function(){} 
          console.log('Search button clicked!', this.origin, this.destination);
    
          // React version: this.props.history.push(`/flights/search/${this.state.origin}/...`)
    
          if( this.origin === '' || this.destination === '' ){
            // console.log('Please select origina and destination!');
    
            // THERE IS NO this.setState() in Vue! You just directly re-assign the
            // value of a piece of state using '=' and Vue magically notices it
            // and triggers a re-render automatically
            this.formErrorMessage = 'Please select an origin and a destination.';
            
            return; // early return to prevent the push() below from happening
          } 
    
    
          this.$router.push({
            name: 'SearchResults', // in router/index.js
            params: {
              // these params imply a route path of '/search/:origin/:destination'
              origin: this.origin,
              destination: this.destination
            }
          });
    
        }, // submitSearch()
    
        validate(){
          // Make the error message disappear when both origin and destination are selected
          if( this.origin !== '' && this.destination !== '' ){
            this.formErrorMessage = '';
          }
    
        }, // validate()
      
      }, // methods
    
    };
    </script>
    
    <style scoped>
      label, button {
        margin: 0 auto;
        display: block;
        margin-bottom: 0.5rem;
      }
    
      .error {
        background-color: orange;
        width: 40vw;
        margin: 1rem auto;
        padding: 1rem;
      }
    
    </style>

