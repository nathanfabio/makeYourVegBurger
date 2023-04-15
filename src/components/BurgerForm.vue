<template>
    <div>
        <p>Message</p>
        <div>
            <form id="burgerForm" @submit="createBurger">
                <div class="inputContainer">
                    <label for="name">Customer's name:</label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Write your name">
                </div>
                <div class="inputContainer">
                    <label for="bread">Choose the bread:</label>
                    <select name="bread" id="bread" v-model="bread" required>
                        <option value="chooseYourBread" disabled hidden>Choose your bread</option>
                        <option v-for="bread in breads" :key="bread.id" :value="bread.type">{{ bread.type }}</option>
                    </select>
                </div>
                <div class="inputContainer">
                    <label for="meat">Choose the meat:</label>
                    <select name="meat" id="meat" v-model="meat">
                        <option value="chooseYourMeat" disabled hidden>Choose your meat</option>
                        <option v-for="meat in meats" :key="meat.id" :value="meat.type">{{ meat.type }}</option>
                    </select>
                </div>
                <div id="optionsContainer" class="inputContainer">
                    <label id="optionsTitle" for="optional">Choose the options:</label>
                    <div class="checkboxContainer" v-for="optional in optionsdata" :key="optional.id">
                        <input type="checkbox" name="options" v-model="options" :value="optional.type">
                        <span>{{ optional.type }}</span>
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
    name: "BurgerForm",
    data() {
        return {
            breads: null,
            meats: null,
            optionsdata: null,
            name: null,
            bread: "chooseYourBread",
            meat: "chooseYourMeat",
            options: [],
            msg: null
        }
    },
    methods: {
        async getIngredients() {
            const req = await fetch("http://localhost:3000/ingredients");

            const data = await req.json();

            this.breads = data.breads;
            this.meats = data.meats;
            this.optionsdata = data.options;
        },

        async createBurger(e) {
            e.preventDefault();

            const data = {
                name: this.name,
                meat: this.meat,
                bread: this.bread,
                options: Array.from(this.options),
                status: "Requested"
            }

            const dataJSON = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJSON
            });

            const res = await req.json();

            this.name = "";
            this.bread = "";
            this.meat = "";
            this.options = "";
        }
    },
    mounted() {
        this.getIngredients()
    },
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

    input {
        border: none;
        border-bottom: .15rem solid #fcba0385;
    }

    input:focus {
        outline: none;
        border-bottom: .15rem solid #fcba03;
    }

    input, select {
        padding: 0.5rem 0.6rem;
        width: 18.75rem;
        font-size: 1rem;
    }
    
    select {
        border-radius: 1rem;
        border: .15rem solid #fcba03;
    }

    select:focus {
        outline: none;
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
        border-radius: .5rem;
        cursor: pointer;
        transition: .8s;
    }

    .submitBtn:hover {
        background-color: transparent;
        color: #222;
    }
</style>