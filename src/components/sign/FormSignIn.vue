<template>
    <form action="#" @submit.prevent="submit" class="sign-in-htm">
        <div class="group">
            <label :class="{ invalid: $v.username.$invalid && $v.username.$dirty }" for="sign-in-user" class="label">Username</label>
            <input 
            :class="{ invalid: $v.username.$invalid && $v.username.$dirty }" 
            id="sign-in-user" 
            type="text" 
            class="input" 
            v-model="username"
            @input="$v.username.$touch()"
            >
            <!-- O $touch do validate vai ficar observando o campo
                Já o dirty é um boolean que sinaliza se ocorreu alguma ação no campo 
             -->
        </div>
        <div class="group">
            <label :class="{ invalid: $v.password.$invalid && $v.password.$dirty }" for="sign-in-pass" class="label">Password</label>
            <input 
            :class="{ invalid: $v.password.$invalid && $v.password.$dirty }" 
            id="sign-in-pass" 
            type="password" 
            class="input" 
            data-type="password" 
            v-model="password"
            @input="$v.password.$touch()">
        </div>
        <div class="group">
            <input id="check" type="checkbox" class="check" v-model="keepSignedIn">
            <label for="check"><span class="icon"></span> Keep me Signed in</label>
        </div>
        <div class="group">
            <input type="submit" class="button" value="Sign In">
        </div>
        <div class="hr"></div>
        <div class="foot-lnk">
            <a href="#forgot">Forgot Password?</a>
        </div>
    </form>
</template>

<script>
import { required } from 'vuelidate/lib/validators'
export default {
    data: () => ({
        username: '',
        password: '',
        keepSignedIn: true
    }),
    mounted(){
        this.$bus.$on('navigate', this.reset);
    },
    validations: {
        username: {
            required
        },
        password: {
            required
        },
    },
    methods: {
        submit() {
            // Os ... (spread operator) cria uma cópia dos dados  
            // Utilizamos esse recurso para que os dados originais não sejam alterados. O dado enviado deixa
            // de ser um observer (perdendo os getters e os setters que o Vue.js colocou) 
            // e passa a ser um objeto puro.  
            // Mas vc pode pensar ..."Pô mais difícil ter um objeto simples assim", geralmente temos objetos com bastante hierarquia.
            //  Nestes casos podemos usar bibliotecas como a Lodash que tem um método chamado cloneDeep
            // que vai percorrer seu objeto recursivamente clonando todas propriedades de todos os objetos e arrays
            // que estiverem dentro dele.
            //Outra maneira de fazer isso, de uma forma state foreign de clonar um objeto antes do ES215.
            // JSON.encode(JSON.stringify(this.$data))
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
                this.keepSignedIn = true;
                this.$v.$reset();
            } 
        }
    },
}
</script>

<style>
</style>