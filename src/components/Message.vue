<template>
    <div class="messageContainer">
        <p>{{ msg }}</p>
    </div>
</template>

<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .messageContainer {
        color: #fcba03;
        background-color: #d39b0023;
        border: 0.125rem solid #ffbb00;
        border-radius: 0.313rem;
        padding: .625rem;
        max-width: 25rem;
        margin: 1.875rem auto;
    }
</style>