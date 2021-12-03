
<script>
    const w = 70;
    const cm = 5; //cursor margin, for cursor select
    const cx = -30; const cy = -300; // center image under cursor
    const ch = 750; const cw = 1490; //canvas height canvas width
	const images = [
		{ id: 1, text: `cat`, name: `cat.png` , width: w},
		{ id: 2, text: `dog`, name: `dog.png` , width: w},
		{ id: 3, text: `dino`, name: `dino.png`, width: w}
	];
    
    const colors = ['magenta','red','orange','yellow','rgb(0,255,0)','green','cyan','blue','rgb(120,0,255)','purple','black','white'];

    let selectedColor = { i: 9, color: colors[9]};

	let selected = images[0];
    
    let top = 1000;
    let bottom;
    let right;
    let left;
    let start = false;
    
    let checkcolors = false;

    
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
        if (start && y > top && y < bottom && x < right && x > left)
            document.getElementById("canvas").innerHTML = document.getElementById("canvas").innerHTML + `<img id="drawn" src="${selected.name}" style="position:absolute; left: ${x}px; top: ${y}px; width: ${selected.width}px">`;
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
    
    function changeCanvasColor(){
        //selectedColor = { i: ((selectedColor.i+1) % colors.length)
        selectedColor.i++;
        selectedColor.i = selectedColor.i % colors.length;
        selectedColor.color = colors[selectedColor.i];
        document.getElementById('canvas').style.backgroundColor = selectedColor.color;
    }
    
    function clearScreen() {
        location.reload(); 
        //document.getElementById("drawn").style.display='none';
    }
    
    function handleStart(event) {
        let coors = getCoords(event);
        left = coors[0];
        top = coors[1] + 25;
        bottom = top + ch - w;
        right = left + cw - w - 30;
        start = true;
        document.getElementById('start').style.display='none';
    }

	function handleSubmit() {
		alert(`answered question ${selected.id} (${selected.text}) with "${answer}"`);
	}
    
    function tester (msg) {
    //on:click={() => tester("hi")}
        console.log(msg);
    }
    console.log("hello");
    
    $: {console.log(`the selected image is ${selected.text}`); }
    
    //$: {document.getElementById('canvas').style.backgroundColor = ${selectedColor.color};}
    //onclick="this.style.backgroundColor=selectedColor.color;"
</script>

<h1>WELCOME</h1>
<h4>Click in the canvas to change its color!</h4>
<p>App by Robin Nash</p>
    


<button value="Select Cursor" on:click={() => toggleMenu('cursor-select')}>Select Cursor</button>
<button on:click={clearScreen}>Clear Screen</button>

{#if checkcolors}
<input type=checkbox style="background-color:#0000ff;background:#0000ff;color:#0000ff">
<input type=checkbox style="background-color:#ff00ff;background:#00ffff;color:#ff0000">
{/if}

<div id="cursor-select" style="display:none; position:relative; top:0px;left:0px;width:{ (w + cm) * images.length + cm}px">
    {#each images as image}
        <img id="cursor" src={image.name} on:click={() => selectCursor(image)} style="display:inline; width:{image.width}px; position:inline; margin-left:{cm}px; margin-top:{cm}px">
    {/each}
</div>

<div style="position:absolute; width:{cw}px; height:{ch}px; margin-bottom:5px;
background-color:#330099;
border:5px solid black;" on:mousemove={drawImage} on:click={changeCanvasColor} id="canvas"> 
<button id="start" on:click={handleStart} style="position:absolute; margin:10px;width:50px;height:50px;background-color:#ff22cc">Start</button>
</div>

  
