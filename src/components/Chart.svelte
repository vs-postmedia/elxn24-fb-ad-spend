<script>
    export let data = [];

    // LIBS
    import { onMount } from 'svelte';

    // VARS
    let width = 500;

    $: console.log(data)
    $: cons = data.length > 0 ? numberWithCommas(data.filter(d => d.page_name === 'Conservative')[0].total) : null;
    $: ndp = data.length > 0 ? numberWithCommas(data.filter(d => d.page_name === 'NDP')[0].total) : null;
    $: green = data.length > 0 ? numberWithCommas(data.filter(d => d.page_name === 'Green')[0].total) : null;
    

    // FUNCTIONS
    function numberWithCommas(x) {
	    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
	}
</script>


<div class="chart-container" bind:clientWidth={width}>
    <div class="list">
        <div class="ndp">
            <p class="party">NDP</p>
            <h1>${ndp}</h1> 
        </div>
        <div class="cons">
            <p class="party">Conservative</p>
            <h1>${cons}</h1> 
        </div>
        <div class="green">
            <p class="party">Green</p>
            <h1>${green}</h1>
        </div>
    </div>
    <p class="timestamp">As of Sept. 21</p>
</div>

<style>
    .chart-container {
        margin-bottom: 25px;
    }
    .list {
        display: flex;
        justify-content: space-around;
        margin-bottom: 5px;
    }
    #app .chart-container h1 {
        font-size: 1.75rem;
    }
    #app .chart-container .party {
        margin-bottom: 5px;
    }
    #app .chart-container .ndp .party,
    #app .chart-container .ndp h1 {
        color: #FD4E27;
    }
    #app .chart-container .green .party,
    #app .chart-container .green h1 {
        color: #009A44;
    }
    #app .chart-container .cons .party,
    #app .chart-container .cons h1 {
        color: #004AAD;
    }
    #app .chart-container .party {
        color: var(--grey03);
        font-size: 0.95rem;
        text-align: center;
        text-transform: uppercase;
    }

    #app .chart-container .timestamp {
        color: var(-grey02);
        font-family: 'BentonSansCond-RegItalic', italic;
        font-size: 0.8rem;
        text-align: center;
    }

    @media screen and (min-width: 500px) {
        #app .chart-container h1 {
            font-size: 2.25rem;
        }
    }
</style>