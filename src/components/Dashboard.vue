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
            <div class="burgerTableRow">
                <div class="orderNumber">1</div>
                <div>Nathan</div>
                <div>3 Cheeses</div>
                <div>NotCo</div>
                <div>
                    <ul>
                        <li> Toffu</li>
                        <li>Cheddar</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status">
                        <option value="">Status:</option>
                    </select>
                    <button class="deleteBtn">Cancel</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Dashboard"
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