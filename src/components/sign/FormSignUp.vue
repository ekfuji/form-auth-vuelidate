<template>
    <form action="#" @submit.prevent="" class="sign-up-htm">
        <div class="group">
            <label for="sign-up-user" class="label">Username</label>
            <input id="sign-up-user" type="text" class="input">
        </div>
        <div class="group">
            <label for="sign-up-pass" class="label">Password</label>
            <input id="sign-up-pass" type="password" class="input" data-type="password">
        </div>
        <div class="group">
            <label for="sign-up-pass-confirmation" class="label">Repeat Password</label>
            <input id="sign-up-pass-confirmation" type="password" class="input" data-type="password">
        </div>
        <div class="group">
            <label for="email" class="label">Email Address</label>
            <input id="email" type="text" class="input">
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
export default {

    mounted() {
        this.$bus.$on('navigate', obj => {
            window.console.log({
                onde: 'signup',
                obj
            });
        });
    },
}
</script>

<style>

</style>