<template>
    <div>
        <Header/>
        <InfoHeader text-color="white"/>
        <router-view/>
        <Footer/>
    </div>
</template>

<script>

    import Header from '.././components/Header.vue'
    import InfoHeader from '.././components/InfoHeader.vue'
    import Footer from '.././components/Footer.vue'

    export default {
        components: {
            Header,
            InfoHeader,
            Footer
        }
    }
</script>

<style scoped>

</style>