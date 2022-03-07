<template>
    <button class="btn btn-outline-primary btn-sm" 
    @click="getReq">{{btnText}}</button>
</template>

<script>
import axios from 'axios'
axios.defaults.headers.get["Content-Type"] = "application/json"

export default {
    name: 'ApiGetButton',
    data(){return {
        btnText:"List Users",
        listOfComments:[],
    }},
    
    methods:{
        getReq: async function(){
            let commentList

            await axios.get('http://localhost:8000/api/users/')
            .then(function(res){
                commentList = res.data
                console.log(commentList)
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
