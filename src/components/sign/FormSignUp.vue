<template>
    <form action="#" @submit.prevent="submit" class="sign-up-htm">
        <div class="group">
            <label :class="{ invalid: $v.username.$invalid && $v.username.$dirty }" for="sign-up-user" class="label">Username</label>
            <input 
            :class="{ invalid: $v.username.$invalid && $v.username.$dirty }" 
            id="sign-up-user" 
            type="text" 
            class="input"
            v-model="username"
            @input="$v.username.$touch()">
        </div>
        <div class="group">
            <label :class="{ invalid: $v.password.$invalid && $v.password.$dirty }" for="sign-up-pass" class="label">Password</label>
            <input 
            :class="{ invalid: $v.password.$invalid && $v.password.$dirty }" 
            id="sign-up-pass" 
            type="password" 
            class="input" 
            data-type="password"
            v-model="password"
            @input="$v.password.$touch()">
        </div>
        <div class="group">
            <label :class="{ invalid: $v.passwordConfirmation.$invalid && $v.passwordConfirmation.$dirty }" for="sign-up-pass-confirmation" class="label">Repeat Password</label>
            <input 
            :class="{ invalid: $v.passwordConfirmation.$invalid && $v.passwordConfirmation.$dirty }" 
            id="sign-up-pass-confirmation" 
            type="password" 
            class="input" 
            data-type="password"
            v-model="passwordConfirmation"
            @input="$v.passwordConfirmation.$touch()">
        </div>
        <div class="group">
            <label :class="{ invalid: $v.email.$invalid && $v.email.$dirty }" for="email" class="label">Email Address</label>
            <input 
            :class="{ invalid: $v.email.$invalid && $v.email.$dirty }" 
            id="email" 
            type="text" 
            class="input"
            v-model="email"
            @input="$v.email.$touch()">
        </div>
        <div class="group">
            <input type="submit" class="button" value="Sign Up">
        </div>
        <div class="hr"></div>
        <div class="foot-lnk">
            <label for="tab-1">Already Member?</label>
        </div>
    </form>
</template>

<script>
import { required, sameAs, email } from 'vuelidate/lib/validators'
export default {
    data: () => ({
        username: '',
        password: '',
        passwordConfirmation: '',
        email: ''
    }),
    validations: {
        username: {
            required
        },
        password: {
            required
        },
        passwordConfirmation: {
            required,
            sameAsPassword: sameAs('password')
        },
        email: {
            required,
            email
        }, 
    },
    mounted() {
        this.$bus.$on('navigate', this.reset);
    },
    methods: {
        submit(){
            if(!this.$v.$invalid){
                this.$emit("doSignIn", { ...this.$data });
            } else {
                this.$v.$touch();
            }
        },
        reset(selected){
            if(selected == 'signup'){
                this.username = '';
                this.password = '';
                this.passwordConfirmation = '';
                this.email = '';
                this.$v.$reset();
            } 
        }
    }
}
</script>

<style>
</style>