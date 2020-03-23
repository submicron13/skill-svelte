<script>
    export let buttonText;
    export let command;
    console.log(command)
    function sendCommand() {
        var xhr = new XMLHttpRequest();
        let url = 'http://localhost:1337/'
        xhr.open("POST", url, true);
        xhr.setRequestHeader('Content-Type', 'application/json');
        xhr.send(JSON.stringify({
            value: command
        }));
    }  
</script>

<style>
.small-margin {
    margin: 3px;
}
</style>

<button class="btn btn-primary small-margin" type="button" on:click={sendCommand}>{buttonText}</button>