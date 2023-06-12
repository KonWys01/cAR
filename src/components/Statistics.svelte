<div class="main-div">
    <div class="stat">
        <img class="licznik" src="../../public/licznik2.png" alt="licznik">
        <h1>{selected}</h1>
        <h2>{value}</h2>
    </div>
    <div class="info">
        <div class="card-display">
            <div class="card-container">
                <Card>
                    <PrimaryAction on:click={() => clicked++}>
                        <Content class="mdc-typography--body2">
                            <h5 class="mdc-typography--headline6" style="margin: 0; font-weight: 400">
                                {advice}
                            </h5>
                            {#if selected !== "Termin przeglądu" }
                                <hr>
                            {/if}
                            <h5 class="mdc-typography--headline6" style="margin: 0; font-weight: 400">
                                {prefered}
                            </h5>
                            <h2 class="mdc-typography--headline6" style="margin: 0; font-weight: 600">{plyn}</h2>
                        </Content>
                    </PrimaryAction>
                </Card>
            </div>
        </div>
    </div>
    <div class="bottom-buttons">
        <Section>
            <IconButton class="material-icons" aria-label="Search" style="width: 55px; height: 55px" on:click={handleClickHamulec}>
                <img src="../../public/hamulcowy.png" style="width: 100%; height: 100%" alt="hamulcowy">
            </IconButton>
            <IconButton class="material-icons" aria-label="Search" style="width: 55px; height: 55px" on:click={handleClickChlodnica}>
                <img src="../../public/chlodnica.png" style="width: 100%; height: 100%" alt="chlodnica">
            </IconButton>
            <IconButton class="material-icons silnikowy" style="width: 55px; height: 55px" on:click={handleClickOlejSilnikowy}>
                <img src="../../public/olej_silnikowy2.png" style="width: 100%; height: 100%" alt="olej_silnikowy" >
            </IconButton>
            <IconButton class="material-icons" aria-label="Search" style="width: 55px; height: 55px" on:click={handleClickKalendarz}>
                <img src="../../public/kalendarz.png" style="width: 100%; height: 100%" alt="kalendarz">
            </IconButton>
        </Section>
    </div>
</div>
<script>
    import IconButton from "@smui/icon-button";
    import {Section} from "@smui-extra/bottom-app-bar";
    import Card, {
        Content,
        PrimaryAction,
    } from '@smui/card';

    let clicked = 0;

    let selected = "Płyn hamulcowy";
    let value = "200km";
    let advice = "Powyższa wartość przedstawia dystans jaki można pokonać bez wymiany płynu hamulcowego";
    let prefered = "Preferowany typ płynu hamulcowego dla twojego modelu samochodu to:";
    let plyn = "K2 Dot 4";

    function handleClickHamulec() {
        selected = "Płyn hamulcowy";
        value = "200km";
        advice = "Powyższa wartość przedstawia dystans jaki można pokonać bez wymiany płynu hamulcowego"
        prefered = "Preferowany typ płynu hamulcowego dla twojego modelu samochodu to:"
        plyn = "borygo START";
    }
    function handleClickChlodnica() {
        selected = "Płyn chłodniczy";
        value = "300km";
        advice = "Powyższa wartość przedstawia dystans jaki można pokonać bez wymiany płynu chłodniczego"
        prefered = "Preferowany typ płynu chłodniczego dla twojego modelu samochodu to:"
        plyn = "K2 Dot 4";
    }
    function handleClickOlejSilnikowy() {
        selected = "Olej silnikowy";
        value = "800km";
        advice = "Powyższa wartość przedstawia dystans jaki można pokonać bez wymiany oleju silnikowego"
        prefered = "Preferowany typ oleju silnikowego dla twojego modelu samochodu to:"
        plyn = "Castrol EDGE";
    }

    function handleClickKalendarz() {
        selected = "Termin przeglądu";
        value= "330dni";
        advice = "Powyższa wartość przedstawia pozostały czas do następnego przeglądu"
        prefered = ""
        plyn = "";
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
        margin: 0;
    }

    h2 {
        font-weight: bold;
        color: #fff;
        font-size: 20px;
        margin-top: 10px
    }

    .bottom-buttons {
        width: 80%;
        height: 103px;
        border: 1px solid;
        margin-left: 10%;
        margin-top: 20%;
    }

    .stat {
        margin-top: 20px;
    }

    .licznik {
        width: 290px;
        height: 235px;
    }

    .card-display {
        width: 80%;
        height: 140px;
        margin-left: 10%;
    }
</style>