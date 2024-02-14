 <template>
        <img class="logo" src="../assets/pangaealogo.png">

    <h1>Sign Up</h1>
    <div class="register">

        <input type="text" v-model="name" placeholder="Enter Name">
        <input type="email" v-model="email" placeholder="Enter Email ID">
        <input type="Password" v-model="password" placeholder="Enter Password">
        <button v-on:click="signUp">
            Sign UP
        </button>
        <p>
            <Router-link to="/login">Login</Router-link>
        </p>
    </div>
</template>
<script>
import axios from 'axios'
import { RouterLink } from 'vue-router';
export default {
    name: 'SignUp',
    data() {
        return {
            name: '',
            email: '',
            password: ''
        };
    },
   methods: {
        async signUp() {
            let result = await axios.post("http://localhost:3000/users", {
                email: this.email,
                name: this.name,
                password: this.password
            });
            console.warn(result);
            if (result.status == 201) {
                localStorage.setItem("user-info", JSON.stringify(result.data));
                this.$router.push({ name: 'Login' });
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
            this.$router.push({ name: 'Login' });
        }
    },
    components: { RouterLink }
}



</script>
<style>
</style>