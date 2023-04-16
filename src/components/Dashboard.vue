<template>
    <div id="burgerTable">
        <div>
            <div id="burgerTableHeading">
                <div class="orderId">#:</div>
                <div>Customer:</div>
                <div>Bread:</div>
                <div>Meat:</div>
                <div>Options:</div>
                <div>Actions:</div>
            </div>
        </div>
        <div id="burgerTableRows">
            <div class="burgerTableRow" v-for="burger in burgers" :key="burger.id">
                <div class="orderNumber">{{ burger.id }}</div>
                <div>{{ burger.name }}</div>
                <div>{{ burger.bread }}</div>
                <div>{{ burger.meat }}</div>
                <div>
                    <ul>
                        <li v-for="(option, index) in burger.options" :key="index">{{ option }}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status">
                        <option v-for="s in status" :key="s.id" value="s.type" :selected="burger.status == s.type">{{ s.type }}</option>
                    </select>
                    <button class="deleteBtn">Cancel</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Dashboard",
    data() {
        return {
            burgers: null,
            burgerId: null,
            status: []
        }
    },
    methods: {
        async getOrders() {
            const req  = await fetch("http://localhost:3000/burgers");

            const data = await req.json();

            this.burgers = data;

            //get the status
            this.getStatus();
        },
        async getStatus() {
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;
        }
    },
    mounted() {
        this.getOrders();
    },
}
</script>

<style scoped>
    #burgerTable {
        max-width: 75rem;
        margin: 0 auto;
    }

    #burgerTableHeading,
    #burgerTableRows,
    .burgerTableRow {
        display: flex;
        flex-wrap: wrap;
    }

    #burgerTableHeading {
        font-weight: bold;
        padding: 0.75rem;
        border-bottom: 0.188rem solid #333;
    }

    #burgerTableHeading div,
    .burgerTableRow div {
        width: 19%;
    }

    .burgerTableRow {
        width: 100%;
        padding: 0.75rem;
        border-bottom: 0.063rem solid #ccc;
    }

    #burgerTableHeading .orderId,
    .burgerTableRow .orderNumber {
        width: 5%;
    }

    select {
        padding: 0.75rem 0.375rem;
        margin-right: 0.75rem;
        border-radius: 1rem;
        border: .15rem solid #fcba03;
    }

    select:focus {
        outline: none;
    }

    .deleteBtn {
        background-color: #222;
        color: #fcba03;
        font-weight: bold;
        border: 0.125rem solid #222;
        padding: 0.625rem;
        font-size: 1rem;
        margin: 0 auto;
        border-radius: .5rem;
        cursor: pointer;
        transition: .5s;
    }

    .deleteBtn:hover {
        background-color: transparent;
        color: #222;
    }
</style>