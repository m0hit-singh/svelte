<script>
    let corona_logo = "./virus.png";
    let stay = "./doc.png";
</script>

    <div class="container">
        <img class="imgsrc" src={corona_logo} alt="corona" />
        <h1>Corona Live Tracker</h1>
        <img class="imgsrc" src={stay} alt="stay" />    
    </div>

<style>
    .container {
        display: flex;
    }

    .container h1 {
        flex-grow: 1;
    }

    .imgsrc {
        height: 100px;
        width: 120px;
        padding: 10px;
    }

    h1 {
        color: #E91E63;
        /* background-color: #B39DDB; */
    }
</style>