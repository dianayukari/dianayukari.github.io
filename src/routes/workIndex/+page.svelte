<script>

    import Menu from "../../lib/components/Menu.svelte"
    import { onMount } from "svelte"
    import { fly } from 'svelte/transition';
    
    let workList = [];

    onMount(
        async () => {
            const response = await fetch('/work_list.json');
            workList = await response.json();
    });

    let activeImgSrc
    let visible = false

    function changeImg(ref) {
        visible = true
        activeImgSrc = "imgs-hover/"+ref+".jpeg"
    }

    function mouseLeaveGrid() {
        activeImgSrc = ""
        visible = false
    }
    

</script>

<div class="home-content">

    <div class="home-descr">
        <div class="vizBox">
            {#if visible}
                <img src={activeImgSrc}>
            {/if}
        </div>

        <div class="home-flex">
            <h1>I'M A DESIGNER CRAFTING VISUAL STORIES USING DATA</h1>
            <p>I enjoy blending <span class="link design">design</span> and <span class="link tech">tech</span> to create data visualizations for print and online media</p>
            <p>I'm originally from Brazil, currently based in the Netherlands</p>
        </div>
    </div>

<div class="grid">
        {#if workList.length > 0}
            {#each workList as d}
                <div class="gridBrick"><a href="work/{d.pos}"><img src="imgs-grid/{d.pos}.jpeg" on:mouseenter={changeImg(d.pos)} on:mouseleave={mouseLeaveGrid}></a></div>
            {/each}
        {/if}

</div>

</div>


<style>

    .vizBox {
        display: block;
        height: 45%;
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 0;
        margin: 0;
        flex: 1;
    }

    .vizBox img {
        max-height: 100%;
        padding: 0;
        margin: 0;
    }

    .vizBox img:hover {
        transition: opacity 2s;
    }

    .home-content {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }

    .home-descr {
        height: 85vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20px;
        justify-content: space-between;
    }

    .home-flex {
        width: 45vw;
    }

    .grid {
        width: 45%;
        height: 85vh;
        display: flex;
        flex-wrap: wrap;
        row-gap: 1%;
        column-gap: 2%;
    }

    .link {
        font-family: Lato;
        text-decoration: underline;
        padding: 2px;
    }

    .gridBrick {
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
        width: 30%;
        height: 25%;
    }

    .gridBrick img {
        width: 200%;
    }


    @media (max-width:650px) {

        .home-descr {
            justify-content: flex-start;
            height: auto;
            margin-bottom: 50px;
        }

        .home-flex {
            width: 100%;
        }

        .vizBox {
            display: none;
        }

        .grid {
            width: 100%;
            height: 100vh;
            justify-content: center;
        }

    }

</style>