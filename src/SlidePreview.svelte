<script>
    let{ numSlides, currentSlide,setCurrentSlide, setLive, deletedSlides} = $props();

    let scrollingWrapper = $state(null);

    let timer = null;

    $effect(() => {

        if(scrollingWrapper)
        {
            clearTimeout(timer);

            timer = setTimeout(() => {
                scrollingWrapper.scrollIntoView({ behavior: "smooth", inline: "center"});
            }, 1000);
        }

    });

    $effect(() => {
    
        console.log("Current value of numSlides prop:", numSlides);
    });

    const slides = $derived(Array.from({ length: numSlides }, (_, i) =>  i+1).filter((slide) => !deletedSlides.includes(slide)));

  </script>


<div class="preview-container">

    <div class="preview">

        {#each slides as slide}

            {#if currentSlide === slide}

                <div class="image-container {currentSlide === slide ? 'active' : ''}" bind:this={scrollingWrapper}>

                    <!-- svelte-ignore a11y_click_events_have_key_events -->
                    <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->

                    <img src={"./slide" + String(slide) + ".png"} alt="Slide preview" onclick={() => {
                        setCurrentSlide(slide);
                        setLive(false);

                    }}/>
                </div>

            {:else}

                <div class="image-container {currentSlide === slide ? 'active' : ''}">

                    <!-- svelte-ignore a11y_click_events_have_key_events -->
                    <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->

                    <img src={"./slide" + String(slide) + ".png"} alt="Slide preview" onclick={() => {
                        setCurrentSlide(slide);
                        setLive(false);

                    }}/>
                </div>

            {/if}
            
            
            

        {/each}

    </div>

</div> 

<style>

@media print{
    .preview{
        flex-direction: column;
         width:100% !important;
    }

    .preview-container{
        width:100% !important;
    }
    
    .image-container{
        height: unset !important;
    }

    .image-container img{
        max-width: 90% !important;
    }
}

.preview-container{
    padding: 1rem;
    background-color:var(--secondary-background);


}

.preview{
    display: flex;
    align-items: center;
    gap: 1rem;
    overflow-x: scroll;
    scroll-behavior: smooth;
    
}

.image-container{
    height: 5rem;
    padding: 0.5rem;
    border-radius:0.5rem 
}

.image-container.active{
    background-color: #3EA05566;

}


.preview-container img{
    flex-shrink: 0;
    object-fit: cover;
    border-radius: 0.25rem;
    box-shadow:0 1px 2px #0000007F;
    max-height: 100%;
}

</style>