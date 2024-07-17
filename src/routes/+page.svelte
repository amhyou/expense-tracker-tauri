<script lang="ts">
    interface Expense {
        name: string;
        cost: number;
        category: Category;
    }
    enum Category {
        Food,
        Housing,
        Transportation,
        Entertainment,
        Health,
        Education,
        Utilities,
        Other,
    }
    let name: string = "";
    let cost: number;
    let category: Category;
    let expenses: Array<Expense> = [];
    $: total = expenses.reduce(
        (sum, currentExpense) => sum + Number(currentExpense.cost),
        0,
    );
    function addExpense() {
        expenses = [{ name, cost, category }, ...expenses];
    }
</script>

<center>
    <h1 class="text-5xl font-bold my-5">Expense Tracker</h1>
    <input
        bind:value={name}
        type="text"
        placeholder="Item name"
        class="input input-bordered input-warning w-1/4 max-w-xs"
    />

    <input
        bind:value={cost}
        type="text"
        placeholder="Cost"
        class="input input-bordered input-warning w-1/4 max-w-xs"
    />
    <select class="select select-warning w-1/4 max-w-xs" bind:value={category}>
        <option>Food</option>
        <option>Housing</option>
        <option>Transportation</option>
        <option>Entertainment</option>
        <option>Health</option>
        <option>Education</option>
        <option>Utilities</option>
        <option>Other</option>
    </select>
    <button on:click={addExpense} class="btn btn-outline btn-info">Add</button>

    <div class="overflow-x-auto mt-5 justify-around">
        <table class="table table-zebra">
            <!-- head -->
            <thead>
                <tr>
                    <th></th>
                    <th>Name</th>
                    <th>Cost</th>
                    <th>Category</th>
                </tr>
            </thead>
            <tbody>
                {#each expenses as item, index}
                    <tr>
                        <th>{index + 1}</th>
                        <td>{item.name}</td>
                        <td>{item.cost} $</td>
                        <td>{item.category}</td>
                    </tr>
                {/each}
            </tbody>
        </table>
    </div>

    <div
        class="fixed bottom-0 left-0 right-0 p-4 bg-gray-800 text-white text-center"
    >
        Total Expense today: {total} $
        <canvas id="myChart" width="400" height="400" bind:this={canvas}
        ></canvas>
    </div>
</center>
