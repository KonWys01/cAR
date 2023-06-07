<div class="flexy">
    <div class="bottom-app-bar-container flexor">
        <div class="flexor-content">
            {#if avaiable === "settings" }
                <Settings/>
            {/if}
            {#if avaiable === "profile" }
                <Profile/>
            {/if}
            {#if avaiable === "Ar" }
                <Ar/>
            {/if}
            {#if avaiable === "carRepair" }
                <CarRepair/>
            {/if}
            {#if avaiable === "statistics" }
                <Statistics/>
            {/if}
        </div>

        <BottomAppBar
                variant="static"
                color={secondaryColor ? 'secondary' : 'primary'}
        >
            <Section>
                <IconButton class="material-icons" aria-label="Search" on:click={handleClickSettings}>
                    settings
                </IconButton
                >
                <IconButton class="material-icons" aria-label="Search" on:click={handleClickProfile}
                >person
                </IconButton
                >
                <IconButton class="material-icons" aria-label="Search" on:click={handleClickAr}
                >center_focus_weak
                </IconButton
                >
                <IconButton class="material-icons" aria-label="Search" on:click={handleClickCarRepair}
                >car_repair
                </IconButton
                >
                <IconButton class="material-icons" aria-label="More" on:click={handleClickStatistics}
                >trending_up
                </IconButton>
            </Section>
            <Section>
            </Section>
        </BottomAppBar>
    </div>
</div>

<script lang="ts">
    import BottomAppBar, {Section} from '@smui-extra/bottom-app-bar';
    import IconButton from '@smui/icon-button';
    import Statistics from "./components/Statistics.svelte";
    import Settings from "./components/Settings.svelte";
    import Profile from "./components/Profile.svelte";
    import Ar from "./components/Ar.svelte";
    import CarRepair from "./components/CarRepair.svelte";

    let secondaryColor = false;
    let avaiable = "statistics";

    function handleClickSettings() {
        avaiable = "settings";
    }
    function handleClickProfile() {
        avaiable = "profile";
    }
    function handleClickAr() {
        avaiable = "Ar";
    }
    function handleClickCarRepair() {
        avaiable = "carRepair";
    }
    function handleClickStatistics() {
        avaiable = "statistics";
    }

</script>

<style>
    .bottom-app-bar-container {
        /*max-width: 480px;*/

        /*width: fit-content;*/
        /*block-size: fit-content;*/
        width: 370px;
        height: 800px;

        overflow: hidden;
        display: inline-flex;
        flex-direction: column;


        /*border: 1px solid;*/
        /*var(--mdc-theme-text-hint-on-background, rgba(0, 0, 0, 0.1));*/
        /*margin: 0 18px 18px 0;*/
        /*background-color: var(--mdc-theme-background, #fff);*/

        /*overflow: auto;*/
        /*display: inline-block;*/
    }

    /*@media (max-width: 480px) {*/
    /*  .bottom-app-bar-container {*/
    /*    margin-right: 0;*/
    /*  }*/
    /*}*/

    .flexy {
        /*display: flex;*/
        flex-wrap: wrap;
        /*width: 365px;*/
    }

    .flexor {
        overflow: hidden;
        display: inline-flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .flexor-content {
        flex-basis: 0;
        height: 0;
        flex-grow: 1;
        overflow: auto;
    }

</style>