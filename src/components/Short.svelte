<script>
    //import
    import Clipboard from "./Clipboard.svelte";


    const copy = () =>{
        const app = new Clipboard({
            target: document.getElementById("clipboard"),
            props: {urlResultado}
        })
        app.$destroy()
    }
    //logica
    let url = '';
    let urlResultado = '';
    let show = false;

    //funcion de llamar la api
    const fetchUrl = async () => {
        const respuesta = await fetch("https://api.shrtco.de/v2/shorten?url=" + url);
        const datos = await respuesta.json();
        urlResultado = datos.result.short_link;
        show = true;
    }

    //varibles de estilos
    const styleInput = 'bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-3 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500';
    const buttonStyle = 'bg-purple-500 hover:bg-purple-400 text-white font-bold py-2 px-10 rounded';
</script>

<div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3">
        <label for="" class="block text-gray-500 font-bold md:text-right pr-4">
            URL to Shorten
        </label>
    </div>
    <div class="md:w-1/3">
        <input type="text" class={styleInput} placeholder="Example://www.mysite.com" bind:value={url}>
    </div>
</div>

<div class="md:flex md:items-center justify-center mt-10">
    <button class={buttonStyle} on:click={fetchUrl}>Consultar</button>
</div>

<!-- if de svelte para que cuando es true muestra eso -->
{#if show}
<div class="md:flex md:items-center justify-center mt-10">
    <input bind:value={urlResultado} class="text-3xl text-pink-500 border-2 border-red-700 mr-3 text-center">
    <button class={buttonStyle} on:click={copy}>Copiar</button>
    <div id="clipboard" />
</div>
{/if}