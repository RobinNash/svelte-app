
<html>
<head>


<script>
	import Select from 'svelte-select';
	
	const items = ['One', 'Two', 'Three'];
	
	const complexItems = [
		{value: 'chocolate', label: 'Chocolate', group: 'Sweet'},
    {value: 'pizza', label: 'Pizza', group: 'Savory'},
    {value: 'cake', label: 'Cake', group: 'Sweet'},
    {value: 'chips', label: 'Chips', group: 'Savory'},
    {value: 'ice-cream', label: 'Ice Cream', group: 'Sweet'}
	];
	
	const groupBy = (item) => item.group;
	const optionIdentifier = 'id';
  const getOptionLabel = (option) => option.name;
  const getSelectionLabel = (option) => option.name;
</script>

<style>
	/* 	CSS variables can be used to control theming.
			https://github.com/rob-balfre/svelte-select/blob/master/docs/theming_variables.md
	*/
	
	.themed {
		--border: 3px solid blue;
		--borderRadius: 10px;
		--placeholderColor: blue;
	}
</style>

<h2>Default</h2>
<Select {items}></Select>


<meta http-equiv="Content-type" content="text/html; charset=utf-8" />
<title>Labs</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
</script>


<style>
* {font-size:1.2em}
</style>



</head>




<script>document.getElementById('body').style.backgroundColor = 'rgb(10,45,255)';</script>

<div style="position:relative;
width:100%px;
height:1000px;
border:5px groove darkgreen;" onmousemove="drawCat(event)" id="canvas"> 
</div>


<script>
function showCoords(event) {
  var cX = event.clientX;
  var sX = event.screenX;
  var cY = event.clientY;
  var sY = event.screenY;
  var coords1 = "client - X: " + cX + ", Y coords: " + cY;
  var coords2 = "screen - X: " + sX + ", Y coords: " + sY;
  document.getElementById("demo").innerHTML = coords1 + "<br>" + coords2;
}
function getCoords(event){
  var cX = event.clientX;
  var sX = event.screenX;
  var cY = event.clientY;
  var sY = event.screenY;
	//return [sX,sY];
//the person said logic was taken from jQuery so maybe look into that
            eventDoc = (event.target && event.target.ownerDocument) || document;
            doc = eventDoc.documentElement;
            body = eventDoc.body;

            event.pageX = event.clientX +
              (doc && doc.scrollLeft || body && body.scrollLeft || 0) -
              (doc && doc.clientLeft || body && body.clientLeft || 0);
            event.pageY = event.clientY +
              (doc && doc.scrollTop  || body && body.scrollTop  || 0) -
              (doc && doc.clientTop  || body && body.clientTop  || 0 );
return  [event.pageX,event.pageY];
}

function drawCat(event){
	coors = getCoords(event);
	x = coors[0];
	y = coors[1];
	//document.write(`<img src="kitten.png" style="display: block; left: 5; top: 5; width: 20px">`);
	//document.write(`<img src="kitten.png" style="position:absolute; left: ${x}; top: ${y}; width: 20px">`);
	document.getElementById("canvas").innerHTML = document.getElementById("canvas").innerHTML + `<img src="kitten.png" style="position:absolute; left: ${x-40}px; top: ${y-40}px; width: 70px">`;
}
</script>


</html>


