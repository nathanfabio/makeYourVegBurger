<template>
<nav>
    <router-link to="/" id="logoUrl">
        <img :src="logo" :alt="alt" id="logo">
    </router-link>
    <router-link to="/">Home</router-link> |
    <router-link to="/orders">Orders</router-link>
</nav> 
</template>

<script>
export default {
    name: "Navbar",
    props: ["logo", "alt"]
}
</script>

<style scoped>
    nav {
        background-color: #222;
        border-bottom: 0.25rem solid #111;
        padding: 1rem 3.2rem;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

    #logoUrl {
        margin: auto;  
        margin-left: 0;
    }

    #logo {
        width: 2.5rem;
        height: 2.5rem;
    }

    nav a {
        color: #fcba03;
        text-decoration: none;
        margin: 0.75rem;
        transition: .5s;
    }

    nav a:hover {
        color: #fff;
    }
</style>