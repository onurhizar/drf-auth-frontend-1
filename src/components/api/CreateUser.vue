<template>
    <button class="btn btn-outline-secondary btn-sm" 
        @click="makePostRequest(_thecomment)">{{btnText}}</button>
</template>

<script>
import axios from 'axios'
axios.defaults.headers.get["Content-Type"] = "application/json"

const apiURL = 'http://127.0.0.1:8000'
const apiRoute = '/api/users/'

export default {
    data(){
        return{
            btnText: "Create User",
            _thecomment: "",
    }},

    methods:{
        async makePostRequest(text){
            let postData = { // prepare the javascript object for post request for API
                username: "vueUser1",
                password: "şifrembudur123"
            }
            let responseStatus
            let _inserted 
            await axios.post(apiURL+apiRoute, postData)
            .then(function(res){
                responseStatus = res.status // 201 if it is successful
                _inserted = res.data // API sends back the inserted object
            })
            .catch(function(error){
                if (error.response.data) console.log(error.response.data)
                else console.log(error)

            }) // FOR DEBUGGING

            if (responseStatus == 201) {
                console.log(_inserted)
                //this.$emit('commentPosted', _inserted) // emit event to append obj to cmmnt list
            }
        }
    }
}
</script>