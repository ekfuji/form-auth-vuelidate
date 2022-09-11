<template>
    <div class="login-wrap">
        <div class="login-html">
            <input 
            value="signin" 
            v-model="navigation" 
            id="tab-1" 
            type="radio" 
            name="tab" 
            class="sign-in" 
            checked
            @change="navigate">
            <label for="tab-1" class="tab">Sign In</label>
            <input 
            value="signup" 
            v-model="navigation" 
            id="tab-2" 
            type="radio" 
            name="tab" 
            class="sign-up"
            @change="navigate">
            <label for="tab-2" class="tab">Sign Up</label>
            <div class="login-form">
                <FormSignIn @doSignIn="doSignIn"/>
                <FormSignUp/> 
            </div>
        </div>
    </div>
</template>

<script>
import FormSignIn from '@/components/sign/FormSignIn.vue';
import FormSignUp from '@/components/sign/FormSignUp.vue';
export default {
    components: { FormSignIn, FormSignUp },
    data: ()=> ({
        navigation: 'signin',
    }),
    methods: {
        navigate(){
            this.$bus.$emit('navigate', this.navigation);
        },
        doSignIn(obj){
            obj.username = "Zezinho";
            console.log(JSON.stringify(obj))
            
        },
        
    }
}
</script>

<style lang="scss" src="@/components/sign/styles.scss"/>
