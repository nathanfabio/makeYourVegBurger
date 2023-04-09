<template>
    <div id="mainBanner">
        <h1>Make Your Veg Burger</h1>
    </div>
    
</template>

<script>
export default {
    name: "Banner"    
}
</script>

<style scoped>
    #mainBanner {
        background-image: url('/public/img/burger.jpg');
        background-position: 100%;
        background-size: cover;
        height: 31.25rem;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #mainBanner h1 {
        color: #fff;
        text-align: center;
        font-size: 3.75rem;
        background-color: #222;
        padding: 1.25rem 2.5rem;
        border-radius: 0 .5rem .5rem 0;
    }
</style>