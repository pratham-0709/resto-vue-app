<template>
    <Header/>
    <h1>HELLO DGFT INDIA - PANGAEA, WELCOME On Add Restaurant Page</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Name" v-model="restaurant.name">
        <input type="text" name="Address" placeholder="Enter Address" v-model="restaurant.address">
        <input type="number" name="Contact" placeholder="Enter Contact" v-model="restaurant.contact">
        <button type="button" v-on:click="addRestaurant()">Add New Restaurant</button>
    </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios';
export default {
    name: 'Add',
    components: {
        Header
    },
    data()
    {
        return {
            restaurant : {
                name:'',
                address:'',
                contact:''
            }
        }
    },
    mounted()
     {
        let user= localStorage.getItem('user-info');
        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }
     },
     methods: {
       async addRestaurant()
        {
            console.warn(this.restaurant)
            const result = axios.post("http://localhost:3000/restaurant",{
                name:this.restaurant.name,
                address:this.restaurant.address,
                contact:this.restaurant.contact,
            });
            if(result.status==201){
                this.$router.push({name:'Home'}) ;
            }
            console.warn("result", result)
        }

     }
}
</script>