<script>
    // COMPONENTS
    import { onMount } from 'svelte';
    import { csvParse } from 'd3-dsv';
    import Chart from "$components/Chart.svelte";

    

    // DATA
    const dataUrl = 'https://vs-postmedia-data.sfo2.digitaloceanspaces.com/elxn/elxn2024/total-fb-ad-spend.csv';

    // VARIABLES
    let data, value;

    async function fetchData(url) {
        const resp = await fetch(url);
        const data = await resp.text();
        
        return csvParse(data);
    }

    async function init() {
        // fetch remote data
        data = await fetchData(dataUrl);
    }

    onMount(init);
</script>

<header>
    <h1>Ad spending for B.C.’s 2024 election on Meta</h1>
    <!-- <p class="subhead">Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p> -->
</header>

<main>
    <h2>Total amount spent</h2>
    <Chart data={data} />

    <h2>Daily ad spending</h2>
    <!-- <p> ($000’s)</p> -->
    <iframe src='https://flo.uri.sh/visualisation/19631149/embed' title='Interactive or visual content' frameborder='0' scrolling='no' style='width:100%;height:350px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe>
</main>

<footer>
    <p class="note">NOTE: Data includes spending by the official Facebook pages for each party. The minimum daily total provided by Facebook is $100, so expenditures may have been less on days showing $100. Data includes ads placed on Facebook, Instagram, WhatsApp and Messenger.</p>
    <p class="source">Source:  <a href="https://www.facebook.com/ads/library/report/?source=onboarding" target="_blank">Facebook Ad Library</a></p>
</footer>
  
<style>
    @import '$css/normalize.css';
    @import '$css/fonts.css';
    @import '$css/colors.css';
    @import '$css/app.css';

    header {
		margin-bottom: 2rem;
	}
	header > h1 {
        line-height: 1.3;
		text-align: center;
	}
	header .subhead {
		margin: 0 auto;
		max-width: 525px;
		text-align: center;
	}
    #app main h2 {
        font-size: 1.35rem;
        margin-bottom: 10px;
        text-align: center;
    }
</style>
