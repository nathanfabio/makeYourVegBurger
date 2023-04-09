<template>
    <div>
        <p>Message</p>
        <div>
            <form id="burgerForm">
                <div class="inputContainer">
                    <label for="name">Customer's name:</label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Write your name">
                </div>
                <div class="inputContainer">
                    <label for="bread">Choose the bread:</label>
                    <select name="bread" id="bread" v-model="bread">
                        <option value="">Choose your bread</option>
                    </select>
                </div>
                <div class="inputContainer">
                    <label for="meat">Choose the meat:</label>
                    <select name="meat" id="meat" v-model="meat">
                        <option value="">Choose your meat</option>
                    </select>
                </div>
                <div id="optionsContainer" class="inputContainer">
                    <label id="optionsTitle" for="optional">Choose the options:</label>
                    <div class="checkboxContainer">
                        <input type="checkbox" name="options" v-model="options" value="Toffu">
                        <span>Toffu</span>
                    </div>
                    <div class="checkboxContainer">
                        <input type="checkbox" name="options" v-model="options" value="Toffu">
                        <span>Toffu</span>
                    </div>
                </div>
                <div class="inputContainer">
                    <input type="submit" class="submitBtn" value="Create my Burger!">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: "BurgerForm"
}
</script>

<style scoped>
    #burgerForm {
        max-width: 25rem;
        margin: 0 auto;
    }

    .inputContainer {
        display: flex;
        flex-direction: column;
        margin-bottom: 1.24rem;
    }

    label {
        font-weight: bold;
        margin-bottom: 1rem;
        color: #222;
        padding: 0.3rem 0.6rem;
        border-left: 0.25rem solid #fcba03;
    }

    input, select {
        padding: 0.3rem 0.6rem;
        width: 18.75rem;
    }

    #optionsContainer {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #optionsTitle {
        width: 100%;
    }

    .checkboxContainer {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 1.25rem;
    }

    .checkboxContainer span, .checkboxContainer input {
        width: auto;
    }

    .checkboxContainer span {
        margin-left: 0.3rem;
        font-weight: bold;
    }

    .submitBtn {
        background-color: #222;
        color: #fcba03;
        font-weight: bold;
        border: 0.1rem solid #222;
        padding: 0.6rem;
        font-size: 1rem;
        margin: 0 auto;
        border-radius: .5rem;
        cursor: pointer;
        transition: .8s;
    }

    .submitBtn:hover {
        background-color: transparent;
        color: #222;
    }
</style>