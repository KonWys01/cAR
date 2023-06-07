<div class="main-div">
    <div class="stat">
        <img class="licznik" src="../../public/licznik2.png" alt="licznik">
        <h1>{selected}</h1>
        <h2>{value}</h2>
    </div>
    <div class="info">

    </div>
    <div class="bottom-buttons">
        <Section>
            <IconButton class="material-icons" aria-label="Search" style="width: 60px; height: 60px" on:click={handleClickHamulec}>
                <img src="../../public/hamulcowy.png" style="width: 100%; height: 100%" alt="hamulcowy">
            </IconButton>
            <IconButton class="material-icons" aria-label="Search" style="width: 60px; height: 60px" on:click={handleClickChlodnica}>
                <img src="../../public/chlodnica.png" style="width: 100%; height: 100%" alt="chlodnica">
            </IconButton>
            <IconButton class="material-icons silnikowy" style="width: 60px; height: 60px" on:click={handleClickOlejSilnikowy}>
                <img src="../../public/olej_silnikowy2.png" style="width: 100%; height: 100%" alt="olej_silnikowy" >
            </IconButton>
            <IconButton class="material-icons" aria-label="Search" style="width: 60px; height: 60px" on:click={handleClickKalendarz}>
                <img src="../../public/kalendarz.png" style="width: 100%; height: 100%" alt="kalendarz">
            </IconButton>
        </Section>
    </div>
</div>
<script>
    import IconButton from "@smui/icon-button";
    import {Section} from "@smui-extra/bottom-app-bar";

    let selected = "Płyn hamulcowy";
    let value = "200km";

    function handleClickHamulec() {
        selected = "Płyn hamulcowy";
        value = "200km";
    }
    function handleClickChlodnica() {
        selected = "Płyn chłodniczy";
        value = "300km";
    }
    function handleClickOlejSilnikowy() {
        selected = "Olej silnikowy";
        value = "800km";
    }

    function handleClickKalendarz() {
        selected = "Termin przeglądu";
        value= "330dni"
    }

</script>
<style>
    .main-div {
        border: 1px solid;
        height: 710px;
    }

    h1 {
        font-weight: bold;
        color: #fff;
        font-size: 32px;
    }

    h2 {
        font-weight: bold;
        color: #fff;
        font-size: 20px;
    }

    .bottom-buttons {
        width: 80%;
        height: 108px;
        border: 1px solid;
        margin-left: 10%;
        margin-top: 20%;
    }

    .stat {
        margin-top: 20px;
        height: 450px;
    }

    .licznik {
        width: 290px;
        height: 235px;
    }
</style>