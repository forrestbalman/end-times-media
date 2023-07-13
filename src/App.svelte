<script>
    import { onMount } from "svelte";

    let videos = [
        {
            name: "green twist",
            thumbnail: "https://img.youtube.com/vi/IlJaMEyUzfo/0.jpg",
            url: "https://www.youtube.com/embed/IlJaMEyUzfo",
        },
        {
            name: "blue twist",
            thumbnail: "https://img.youtube.com/vi/aoNbD7SyDUw/0.jpg",
            url: "https://www.youtube.com/embed/aoNbD7SyDUw",
        },
        {
            name: "red twist",
            thumbnail: "https://img.youtube.com/vi/RaVW5nu61-c/0.jpg",
            url: "https://www.youtube.com/embed/RaVW5nu61-c",
        },
        {
            name: "green reign",
            thumbnail: "https://img.youtube.com/vi/YFh_PZsy97s/0.jpg",
            url: "https://www.youtube.com/embed/YFh_PZsy97s",
        },
        {
            name: "blue reign",
            thumbnail: "https://img.youtube.com/vi/QdCZYD7g0K4/0.jpg",
            url: "https://www.youtube.com/embed/QdCZYD7g0K4",
        },
        {
            name: "red reign",
            thumbnail: "https://img.youtube.com/vi/u8h3vpkg3DY/0.jpg",
            url: "https://www.youtube.com/embed/u8h3vpkg3DY",
        },
        {
            name: "blue from red green",
            thumbnail: "https://img.youtube.com/vi/AqAmbcp_BFQ/0.jpg",
            url: "https://www.youtube.com/embed/AqAmbcp_BFQ",
        },
        {
            name: "green from blue red",
            thumbnail: "https://img.youtube.com/vi/tIWZUHOSC0g/0.jpg",
            url: "https://www.youtube.com/embed/tIWZUHOSC0g",
        },
        {
            name: "red from green blue",
            thumbnail: "https://img.youtube.com/vi/fOgAOlp39i8/0.jpg",
            url: "https://www.youtube.com/embed/fOgAOlp39i8",
        },
        {
            name: "green heaven",
            thumbnail: "https://img.youtube.com/vi/TZLuh81Pdv4/0.jpg",
            url: "https://www.youtube.com/embed/TZLuh81Pdv4",
        },
        {
            name: "blue heaven",
            thumbnail: "https://img.youtube.com/vi/Cro2FzZ270I/0.jpg",
            url: "https://www.youtube.com/embed/Cro2FzZ270I",
        },
        {
            name: "red heaven",
            thumbnail: "https://img.youtube.com/vi/WwqZVv9xCCY/0.jpg",
            url: "https://www.youtube.com/embed/WwqZVv9xCCY",
        },
        {
            name: "green solo",
            thumbnail: "https://img.youtube.com/vi/2S9XA-A7gPw/0.jpg",
            url: "https://www.youtube.com/embed/2S9XA-A7gPw",
        },
        {
            name: "blue solo",
            thumbnail: "https://img.youtube.com/vi/mQOg7ApMmUs/0.jpg",
            url: "https://www.youtube.com/embed/mQOg7ApMmUs",
        },
        {
            name: "red solo",
            thumbnail: "https://img.youtube.com/vi/5a_n2vt9KuU/0.jpg",
            url: "https://www.youtube.com/embed/5a_n2vt9KuU",
        },
    ];
    let showLightbox = false;
    let activeVideo = "https://www.youtube.com/embed/IlJaMEyUzfo";
    let iframeRef;

    const toggleLightbox = (url) => {
        showLightbox = !showLightbox;
        if (showLightbox) {
            activeVideo = url;
        } else {
            // Clear the iframe source when hiding the lightbox
            activeVideo = "";
        }
    };

    onMount(() => {
        // When the iframe finishes loading, set the active video URL
        iframeRef.addEventListener("load", handleIframeLoad);
    });

    const handleIframeLoad = () => {
        activeVideo = iframeRef.src;
    };
</script>

<main class="w-100 h-100 d-flex justify-content-center align-items-center bg-dark">
    <div class="wrapper">
        <div class="row">
            {#each videos as video}
                <!-- svelte-ignore a11y-no-static-element-interactions -->
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <div class="tile col-4 p-0 border border-secondary" on:click={() => toggleLightbox(video.url)}>
                    <img src={video.thumbnail} alt={video.name} class="w-100 h-100" />
                </div>
            {/each}
        </div>
    </div>
</main>

<div class="{showLightbox === false ? 'd-none' : ''} lightbox-bg position-fixed top-0 start-0 w-100 h-100" />
<div class="{showLightbox === false ? 'd-none' : ''} lightbox position-fixed top-0 start-0 w-100 h-100 d-flex justify-content-center align-items-center">
    <!-- svelte-ignore a11y-missing-attribute -->
    <iframe id="video-iframe" src={activeVideo} frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen class="{showLightbox === false ? 'd-none' : ''} w-75 h-75" bind:this={iframeRef} />
</div>
<div class="{showLightbox === false ? 'd-none' : ''} lightbox-close position-fixed top-0 end-0 m-3">
    <button class="btn text-light fs-3" on:click={toggleLightbox}>X</button>
</div>

<style>
    .wrapper {
        width: 42vh;
    }

    .tile {
        height: 8vh;
        transition: scale 0.15s ease-in-out;
    }

    @media (max-height: 500px) {
        .wrapper {
            width: 54vh;
        }

        .tile {
            height: 11vh;
        }
    }

    .tile:hover {
        scale: 0.95;
    }

    img {
        object-fit: cover;
    }

    .lightbox-bg {
        background-color: rgba(0, 0, 0, 0.8);
    }
</style>
