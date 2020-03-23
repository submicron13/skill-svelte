<script>
  import io from 'socket.io-client';
  const socket = io('http://localhost:1337');
  import Kontroller from './Kontroller.svelte'
function sendCommand(command) {
    var xhr = new XMLHttpRequest();
    let url = 'http://localhost:1337/'
    xhr.open("POST", url, true);
    xhr.setRequestHeader('Content-Type', 'application/json');
    xhr.send(JSON.stringify({
        value: command
    }));
}  
  function imageClicked(event) {
 	const xCoordinate = event.offsetX;
    const yCoordinate = event.offsetY;
	// const cadImage = document.getElementById('cadImage').value;
	// const flipX = xCoordinate;
	const flipY = 768 - yCoordinate;
	// const test = xCoordinate + ',' + yCoordinate + '\n' + flipX + ',' + flipY; 
	// console.log(test)
	const command = 'list(RDsccGotCoords() ' + xCoordinate + ' ' + flipY + ')'
	sendCommand(command)
	// cartesianx = screenx - screenwidth / 2;
	// cartesiany = -screeny + screenheight / 2;
  }

</script>
<svelte:head>
<!-- <script src="/socket.io/socket.io.js"></script>
<script>let socket = io();</script> -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootswatch/4.4.1/darkly/bootstrap.min.css" />
</svelte:head>
<main>
<div class="row">
  <div class="col-3"><Kontroller /></div>
  <div class="col-9"><h1><img id="cadImage" src="http://localhost:1337/test.jpg" alt="" on:click={(event) => imageClicked(event)}></h1></div>
</div>

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>