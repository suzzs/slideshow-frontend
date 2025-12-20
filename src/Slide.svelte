<script>
    import { untrack } from "svelte"; 

    const DISTANCE_THRESHOLD = 30;

    let animateImage = $state(false);
    

    let { currentSlide, setCurrentSlide, isLive, numSlides } = $props();

    let initialX = 0;

    function handlePointerDown(event){

        initialX= event.clientX;
console.log(event);
    }

    function handlePointerUp(event){
        console.log(event); 

        let finalX = event.clientX;

        const diff = finalX - initialX;

        if(Math.abs(diff) > DISTANCE_THRESHOLD)
        {

            if(diff > 0)
            {
                if(currentSlide > 1)
                {
                    setCurrentSlide(currentSlide-1);
                }
            }
            else
            {
                if(currentSlide < numSlides)
                {
                    setCurrentSlide(currentSlide+1);
                }
                
            }

        }

    }

    $effect(()=>{

        currentSlide;

        untrack(()=>{


        if(isLive){

            animateImage = true;


            setTimeout(() => {

                animateImage = false;

            }, 1000);

        }

        })

})

</script>

<div class="slides">
   {#if currentSlide>0}
    <img class={ animateImage ? "slide" : ' ' } src={"./slide" + currentSlide + ".png"} alt={"Slide " + currentSlide} onpointerdown={handlePointerDown} onpointerup={handlePointerUp} />
    {:else}
    <div class="no-slides">
        <svg width="10rem" height="10rem" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path fill-rule="evenodd" clip-rule="evenodd" d="M23 4C23 2.34315 21.6569 1 20 1H4C2.34315 1 1 2.34315 1 4V20C1 21.6569 2.34315 23 4 23H20C21.6569 23 23 21.6569 23 20V4ZM21 4C21 3.44772 20.5523 3 20 3H4C3.44772 3 3 3.44772 3 4V20C3 20.5523 3.44772 21 4 21H20C20.5523 21 21 20.5523 21 20V4Z" />
            <path d="M4.80665 17.5211L9.1221 9.60947C9.50112 8.91461 10.4989 8.91461 10.8779 9.60947L14.0465 15.4186L15.1318 13.5194C15.5157 12.8476 16.4843 12.8476 16.8682 13.5194L19.1451 17.5039C19.526 18.1705 19.0446 19 18.2768 19H5.68454C4.92548 19 4.44317 18.1875 4.80665 17.5211Z" />
            <path d="M18 8C18 9.10457 17.1046 10 16 10C14.8954 10 14 9.10457 14 8C14 6.89543 14.8954 6 16 6C17.1046 6 18 6.89543 18 8Z" />
        </svg>
     </div>
    {/if}

     <button class ="save" onclick={()=>{ window.print(); }}>Save as PDF</button>
</div>

<style>

@media print{
    .slides{
        display:none !important;

    }
}

    .slides{
        display:flex;
        justify-content: center;
        align-items: center;
        padding: 1rem;
        cursor: grab;
        flex-grow: 1;
        position: relative;
    }
    .slide{
        animation: appear 400ms ease-in-out forwards;
    }

    .slides:active{
        cursor:grabbing;
    }

    img {
        max-width: 100%;
        max-height: 100%;
        box-shadow: 0 1px 2px rgba(0,0,0,0.5);
        border-radius: 8px;
        touch-action: pinch-zoom;
    }

    .no-slides{
        height:40dvh;
        background-color: #56AE5755;
        flex-grow: 1;
        border-radius: 1rem;
        display:flex;
        align-items: center;
        justify-content: center;
        font-size: 2.8rem;
        font-weight: bold;
        text-align: center;
        padding: 1rem;
    }

    .no-slides svg path{
        fill: #2A572B;
    }

    .save{
    background-color: #56AE5799;
    border:none;
    padding:0.5rem;
    border-radius: 100vw;
    color: white;
    font-weight: bold;
    position: absolute;
    right: 1rem;
    bottom: 1rem;

    }

    

    @keyframes appear{
        from {
            
            transform: scale(0.2) translateY(-100%);
            opacity: 0;
        }
        to{
            transform: scale(1) translateY(0);
            opacity: 1;
        }
    }
</style>
