<template>
    <div id="burgerTable">
        <Message :msg="msg" v-show="msg" />
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
                    <select name="status" class="status" @change="updatedBurger($event, burger.id)">
                        <option v-for="s in status" :key="s.id" :value="s.type" :selected="burger.status == s.type">{{ s.type }}</option>
                    </select>
                    <button class="deleteBtn" @click="deleteBurger(burger.id)">Cancel</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue'
export default {
    name: "Dashboard",
    data() {
        return {
            burgers: null,
            burgerId: null,
            status: [],
            msg: null
        }
    },
    components: {
        Message
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
        },
        async deleteBurger(id) {
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            //status message
            this.msg = `Order successfully removed!`;

            //clear message
            setTimeout(() => this.msg = "", 3000);

            this.getOrders();
        },
        async updatedBurger(event, id) {
            const option = event.target.value;

            const dataJson = JSON.stringify({ status: option });

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            //status message
            this.msg = `Order N°${res.id} has been updated to "${res.status}"!`;

            //clear message
            setTimeout(() => this.msg = "", 3000);
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