<script>
    import { onMount } from "svelte";
	

	
	import Header from "./Header.svelte";
	import Slide from "./Slide.svelte";
	import SlidePreview from "./SlidePreview.svelte";

	let isLive = $state(true);


	let numSlides = $state(0);

	let currentSlide = $state(0);

	let deletedSlides = $state([]);

	

	function setLive(value){
		isLive =value
	}

    function setCurrentSlide(value){
        currentSlide=value;
    }


    function handleKeyDown(event) {
        console.log("Key pressed:", event.key, "Current slide index:", currentSlide);

        if (event.key === "ArrowRight")
		{

            if(currentSlide < numSlides)
			{
                currentSlide += 1;

            }
        } 
        
        if (event.key === "ArrowLeft") {

            if (currentSlide > 1) {

                currentSlide -= 1;
            }
			
        }
    }


    onMount(() =>{


		const socket = new WebSocket('ws://10.10.254.169:1234');

			socket.addEventListener("message" ,(event)=>{

				let receivedMessage = JSON.parse(event.data);



				if(receivedMessage.message_type === "slidesInfo"){

					numSlides = receivedMessage.current_state.num_slides;

					deletedSlides = receivedMessage.current_state.deleted_slides;
				}



				else if(receivedMessage.message_type === "slideAdded"){
					
					numSlides=receivedMessage.current_state.num_slides;

					if(isLive){
						currentSlide =numSlides;
					}

				}


				else if(receivedMessage.message_type === "slideDeleted"){

					deletedSlides = receivedMessage.current_state.deleted_slides;

					if(deletedSlides.includes(currentSlide)){
						currentSlide = 0;
					}

				}
			});
		})

	
</script>



<svelte:window onkeydown={handleKeyDown} />

<div class="app">

	<Header {isLive} {setLive} />

	<Slide {currentSlide} {setCurrentSlide} {isLive} {numSlides} />

	<SlidePreview {numSlides} {currentSlide}  {setCurrentSlide} {setLive} {deletedSlides} />

</div>




<style>

	.app {
		height: 100dvh;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		background-color: var(--primary-background);
	}
</style>
