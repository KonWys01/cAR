<script>
    import IconButton from "@smui/icon-button";
    import {Section} from "@smui-extra/bottom-app-bar";
</script>

<div class="main-div">
    <p>Statistics</p>
    <div class="bottom-buttons">
        <Section>
            <IconButton class="material-icons" aria-label="Search" style="width: 60px; height: 60px">
                <img src="../../public/hamulcowy.png" style="width: 100%; height: 100%" alt="hamulcowy">
            </IconButton>
            <IconButton class="material-icons" aria-label="Search" style="width: 60px; height: 60px">
                <img src="../../public/chlodnica.png" style="width: 100%; height: 100%" alt="chlodnica">
            </IconButton>
            <IconButton class="material-icons silnikowy" style="width: 60px; height: 60px">
                <img src="../../public/olej_silnikowy2.png" style="width: 100%; height: 100%" alt="olej_silnikowy">
            </IconButton>
            <IconButton class="material-icons" aria-label="Search" style="width: 60px; height: 60px">
                <img src="../../public/kalendarz.png" style="width: 100%; height: 100%" alt="kalendarz">
            </IconButton>
        </Section>
    </div>
</div>

<style>
    .main-div {
        border: 1px solid;
        height: 710px;
    }

    .bottom-buttons {
        width: 80%;
        height: 108px;
        border: 1px solid;
        margin-left: 10%;
        margin-top: 100%;
        /*padding: 0;*/
    }

    /*.silnikowy {*/
    /*    width: 50px;*/
    /*    height: 50px;*/
    /*}*/
</style>