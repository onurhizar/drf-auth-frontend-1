<template>
    <button class="btn btn-outline-primary btn-sm" 
    @click="getReq">{{btnText}}</button>
</template>

<script>
import axios from 'axios'
axios.defaults.headers.get["Content-Type"] = "application/json"

const apiURL = 'http://127.0.0.1:8000'
const apiRoute = '/api/protected-test/'

function getCookie(cookieKey) {
    const cookies = document.cookie.split('; ')
    let cookieValue = undefined
    cookies.forEach(function(cookie) {
        if (cookie.startsWith(`${cookieKey}=`)) {
            cookieValue = cookie.split('=')[1]
        }
    })
    return cookieValue
}

export default {
    name: 'ApiGetButton',
    data(){return {
        btnText:"Protected Route",
        listOfComments:[],
    }},
    
    methods:{
        getReq: async function(){
            let response

            //check cookie if exists, then use it for header
            let config = {}
            let cookieValue = getCookie('auth_token')
            if (cookieValue) config.headers={
                'Authorization': `Token ${cookieValue}`
            }

            await axios.get(apiURL + apiRoute, config)
            .then(function(res){
                response = res.data
                console.log(response)
            })
            .catch(function(error){
                if (error.response.data) console.log(error.response.data)
                else console.log(error)
            })
            
            //this.$emit('guncel',commentList)  // emit a custom event
        }
    },
}
</script>
