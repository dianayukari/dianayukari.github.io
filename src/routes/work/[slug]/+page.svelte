<script>

    import { page } from '$app/stores';
    import { onMount } from 'svelte';

    $: slug = $page.params.slug

    let boxHeight
    let workPiece = {};

    onMount(async () => {
    const response = await fetch(`/data/${slug}.json`);

    if (response.ok) {
        workPiece = await response.json();

    } else {
        workPiece = { title: 'Not Found', description: 'The requested work piece could not be found.' };
    }    
    });    


</script>

<div class="mainContainer">

    <div class="headImage" style="height:{boxHeight}px;">
        <img src={workPiece.headImage}>
    </div>

    <div class="workDescrBox" bind:clientHeight={boxHeight}>

        <p class="ano whiteText">{workPiece.ano}</p>
        <p class="titulo whiteText">{workPiece.title}</p>
        <p class="descrText whiteText">{workPiece.description}</p>
        <p class="toolboxTitle whiteText">TOOLBOX</p>
        <div class="toolbox whiteText"><p class="whiteText">{workPiece.toolbox}</p></div>

        <button>see it live</button>

    </div>
</div>

<div class="blogContainer">
    <div class="imgSeq"></div>
</div>



<style>

    .mainContainer {
        display: flex;
        align-items: flex-start;
        overflow: hidden;
    }

    .headImage {
        overflow: hidden;
        width: 40%;
        padding: 0;
    }

    .workDescrBox {
        padding: 15px 40px 40px 40px;
        background-color: #012623;
        flex-grow: 1;
    }

    .ano {
        font-size: 14px;
    }

    .titulo {
        font-size: 24px;
        font-weight: 700;
    }

    .toolboxTitle {
        margin: 30px 0 0 0;
    }

    .toolbox {
        margin: 0;
    }

    .descrText {
        font-size: 14px;
        width: 45vw;
    }

    .blogContainer {
        background-color: blue;
        width: 80vw;
        height: 1000px;
        margin: 40px auto;
    }

    @media (max-width:650px) {

        .mainContainer {
            flex-wrap: wrap;
            width: 100%;
        }

        .headImage {
            /* width: 100%; */
            max-height: 200px;
            overflow: visible;
        }

        .workDescrBox {
            width: 100%;
        }

        .descrText {
        font-size: 14px;
        width: 100%;
    }


    }


</style>