<script>
import Button from './Button.svelte'

let buttons = [
    {
        text: 'hello',
        func: 'test()'
    },
    {
        text: 'hello2',
        func: 'test2()'
    },
    {
        text: 'hello',
        func: 'test()'
    },
    {
        text: 'hello2',
        func: 'test2()'
    },
    {
        text: 'hello',
        func: 'test()'
    },
    {
        text: 'hello2',
        func: 'test2()'
    }
]
function sendCommand(command) {
    var xhr = new XMLHttpRequest();
    let url = 'http://localhost:1337/'
    xhr.open("POST", url, true);
    xhr.setRequestHeader('Content-Type', 'application/json');
    xhr.send(JSON.stringify({
        value: command
    }));
}  
function refreshImage() {
    sendCommand('RDsccExportImage()')
}
</script>

<style>
.small-margin {
    margin: 3px;
}
</style>

<h4>Command & Control</h4>
<button class="small-margin btn btn-primary btn-block" on:click={refreshImage}>Refresh Image</button>
{#each buttons as but}
    <Button buttonText={but.text} command={but.func}/>
{/each}