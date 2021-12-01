
<script>
//https://stackoverflow.com/questions/56483209/import-css-in-node-modules-to-svelte
//https://svelte.dev/blog/the-easiest-way-to-get-started  //install svelte
//https://www.codegrepper.com/code-examples/javascript/get+mouse+position+javascript  cursor function i stole
    const w = 70;
    const cm = 5; //cursor margin, for cursor select
    const cx = 0; const cy = 0; // center image under cursor
	let images = [
		{ id: 1, text: `cat`, name: `cat.png` , width: w},
		{ id: 2, text: `dog`, name: `dog.png` , width: w},
		{ id: 3, text: `dino`, name: `dino.png`, width: w}
	];

	let selected = images[0];
    
    let top = 1000;
    let start = false;
    
    let colors = false;

    
    function getCoords(event){
    //the person said logic was taken from jQuery so maybe look into that
                let eventDoc = (event.target && event.target.ownerDocument) || document;
                let doc = eventDoc.documentElement;
                let body = eventDoc.body;

                let pageX = event.clientX +
                  (doc && doc.scrollLeft || body && body.scrollLeft || 0) -
                  (doc && doc.clientLeft || body && body.clientLeft || 0);
                let pageY = event.clientY +
                  (doc && doc.scrollTop  || body && body.scrollTop  || 0) -
                  (doc && doc.clientTop  || body && body.clientTop  || 0 );
    return  [pageX + cx, pageY + cy];
    }

    function drawImage(event){
        let coors = getCoords(event);
        let x = coors[0];
        let y = coors[1];
        if (y > top && start)
            document.getElementById("canvas").innerHTML = document.getElementById("canvas").innerHTML + `<img src="${selected.name}" style="position:absolute; left: ${x}px; top: ${y}px; width: ${selected.width}px">`;
    }

    function selectCursor(image){
        selected = image;
        toggleMenu('cursor-select');
    }

    function toggleMenu(id){
        let on = document.getElementById(id).style.display;
        console.log('hi');
        if (on == "none")
            document.getElementById(id).style.display='block';
        else
            document.getElementById(id).style.display='none';
    }
    
    function handleStart(event) {
        top = getCoords(event)[1];
        start = true;
        document.getElementById('start').style.display='none';
    }

	function handleSubmit() {
		alert(`answered question ${selected.id} (${selected.text}) with "${answer}"`);
	}
    
    function tester (msg) {
        console.log(msg);
    }
    console.log("hello");
    
    $: {console.log(`the selected image is ${selected.text}`); }
</script>

<h2>This is a paragraph.</h2>

<style>
	h2 { background-color: #ffaaff }
</style>

<button value="Select Cursor" on:click={() => toggleMenu('cursor-select')}>Select Cursor</button>
<button on:click={() => tester("hi")}>Clear Screen</button>

{#if colors}
<input type=checkbox style="background-color:#0000ff;background:#0000ff;color:#0000ff">
<input type=checkbox style="background-color:#ff00ff;background:#00ffff;color:#ff0000">
{/if}

<div id="cursor-select" style="display:none; position:relative; background-color: #505050; top:0px;left:0px;width:{w * 3 + 5 * 3}px">
    {#each images as image}
        <img id="cursor" src={image.name} on:click={() => selectCursor(image)} style="display:inline; width:{image.width}px; position:inline">
    {/each}
</div>

<div style="position:absolute;
width:1000px;
height:1000px;
border:5px groove black;" on:mousemove={drawImage} id="canvas"> 
<button id="start" on:click={handleStart} style="position:absolute; margin:10px;width:50px;height:50px">Start</button>
</div>
    
    
    
  