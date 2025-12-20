<script>
    let {isLive ,setLive} = $props();

    function sayHello(name)
    {
        alert("Hello, " + name);
    }

    

</script>



<header class= "header">

    <div class="logo-container">

        <svg class="logo" width="2rem" height="2rem" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M6.59961 11.3974C6.59961 8.67119 6.59961 7.3081 7.44314 6.46118C8.28667 5.61426 9.64432 5.61426 12.3596 5.61426H15.2396C17.9549 5.61426 19.3125 5.61426 20.1561 6.46118C20.9996 7.3081 20.9996 8.6712 20.9996 11.3974V16.2167C20.9996 18.9429 20.9996 20.306 20.1561 21.1529C19.3125 21.9998 17.9549 21.9998 15.2396 21.9998H12.3596C9.64432 21.9998 8.28667 21.9998 7.44314 21.1529C6.59961 20.306 6.59961 18.9429 6.59961 16.2167V11.3974Z" class="primary-logo"/>
            <path opacity="0.5" d="M4.17157 3.17157C3 4.34315 3 6.22876 3 10V12C3 15.7712 3 17.6569 4.17157 18.8284C4.78913 19.446 5.6051 19.738 6.79105 19.8761C6.59961 19.0353 6.59961 17.8796 6.59961 16.2167V11.3974C6.59961 8.6712 6.59961 7.3081 7.44314 6.46118C8.28667 5.61426 9.64432 5.61426 12.3596 5.61426H15.2396C16.8915 5.61426 18.0409 5.61426 18.8777 5.80494C18.7403 4.61146 18.4484 3.79154 17.8284 3.17157C16.6569 2 14.7712 2 11 2C7.22876 2 5.34315 2 4.17157 3.17157Z" class="secondary-logo"/>
        </svg>

        <h1 class="title">Slideshow</h1>
    </div>


    <div class="live-container">
    
        {#if isLive}
        <svg class="live-icon" width= "24" height = "24" viewBox ="0 0 24 24" fill ="grey" xmlns="http://www.w3.org/2000/svg">
                <circle cx="12" cy="12" r="4" />
        </svg>
            <p>Live</p>
        
        {:else}
            <button class="go-live" onclick={() => setLive(true)}>Go Live</button>
        {/if}
       

    </div>


</header>






<style>

    @media print{
        .header{
            display:none !important;
        }
    }

.header{
    background-color :var(--secondary-background);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
   

}

.logo-container{
    display: flex;
    gap: 0.5rem;
}

.live-icon{
    height:24px;
    width: 24px;
   
}

.live-icon circle{
    fill:#FF3F00DD;

}

.title{
        color: var(--primary-logo-color);
        font-size: 2rem;
        margin: 0;
}

.logo{
    transform: rotate(90deg);

}

p{
    margin:0;
    color:#FF3F00DD;
}

.live-container{
    display:flex;
    align-items: center;    
}


.primary-logo{
fill: var(--primary-logo-color);
}

.secondary-logo{
    fill: var(--secondary-logo-color);
}

.go-live{
    border:none;
    background-color:#FF3F0099;
    padding:0.5rem;
    border-radius: 100vw;
    color: white;
    font-weight: bold;
}


</style>