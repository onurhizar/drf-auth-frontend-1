<template>
    <button class="btn btn-outline-primary btn-sm" 
    @click="getReq">{{btnText}}</button>
</template>

<script>
import axios from 'axios'

axios.defaults.headers.get["Content-Type"] = "application/json"
const apiURL = 'http://localhost:8000'
const apiRoute = '/api/setcookie-test/'

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
        btnText:"Get Cookie",
    }},
    
    methods:{
        getReq: async function(){
            let response

            await axios.get(apiURL + apiRoute, {crossDomain: true})
            .then(function(res){
                response = res.data
                document.cookie = `auth_token=${response["token"]}; Max-Age=60; Path=/`
                
                let cookieValue = getCookie('auth_token')
                if (cookieValue) console.log(cookieValue)

                
            })
            .catch(function(error){
                if (error.response.data) console.log(error.response.data)
                else console.log(error)
            })
        }
    },
}
</script>
