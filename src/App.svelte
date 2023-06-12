<script lang="ts">
    import BottomAppBar, {Section} from '@smui-extra/bottom-app-bar';
    import IconButton from '@smui/icon-button';
    import Statistics from './components/Statistics.svelte';
    import Settings from './components/Settings.svelte';
    import Profile from './components/Profile.svelte';
    import Ar from './components/Ar.svelte';
    import CarRepair from './components/CarRepair.svelte';

    let secondaryColor = false;
    let avaiable = 'statistics';

    function handleClickSettings() {
        avaiable = 'settings';
    }

    function handleClickProfile() {
        avaiable = 'profile';
    }

    function handleClickAr() {
        avaiable = 'Ar';
    }

    function handleClickCarRepair() {
        avaiable = 'carRepair';
    }

    function handleClickStatistics() {
        avaiable = 'statistics';
    }

    window.addEventListener('resize', function () {
        var fullHeightDiv = document.getElementsByClassName(
            'full-height'
        )[0] as HTMLElement;
        if (fullHeightDiv) fullHeightDiv.style.height = window.innerHeight + 'px';
    });

    window.addEventListener('DOMContentLoaded', (event) => {
        var fullHeightDiv = document.getElementsByClassName(
            'full-height'
        )[0] as HTMLElement;
        if (fullHeightDiv) fullHeightDiv.style.height = window.innerHeight + 'px';
    });
</script>

<div class="container full-height">
    <div class="content">
        {#if avaiable === 'settings'}
            <Settings/>
        {/if}
        {#if avaiable === 'profile'}
            <Profile/>
        {/if}
        {#if avaiable === 'Ar'}
            <Ar/>
        {/if}
        {#if avaiable === 'carRepair'}
            <CarRepair/>
        {/if}
        {#if avaiable === 'statistics'}
            <Statistics/>
        {/if}
    </div>

    <div class="bottombar">
        <BottomAppBar
                variant="static"
                color={secondaryColor ? 'secondary' : 'primary'}
        >
            <Section>
                <div class="bottom-button">
                    <IconButton
                            class="material-icons"
                            aria-label="Search"
                            on:click={handleClickSettings}
                    >
                        settings
                    </IconButton>
                </div>
                <div class="bottom-button">
                    <IconButton
                            class="material-icons"
                            aria-label="Search"
                            on:click={handleClickProfile}
                    >person
                    </IconButton>
                </div>
                <div class="bottom-button">
                    <IconButton
                            class="material-icons"
                            aria-label="Search"
                            on:click={handleClickAr}
                    >center_focus_weak
                    </IconButton>
                </div>
                <div class="bottom-button">
                    <IconButton
                            class="material-icons"
                            aria-label="Search"
                            on:click={handleClickCarRepair}
                    >car_repair
                    </IconButton>
                </div>
                <div class="bottom-button2">

                    <IconButton
                            class="material-icons"
                            aria-label="More"
                            on:click={handleClickStatistics}
                    >trending_up
                    </IconButton>
                </div>


            </Section>
            <Section/>
        </BottomAppBar>
    </div>
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
        width: 100%;
    }

    .content {
        flex-grow: 1;
    }

    .bottombar {
        margin-top: auto;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .bottom-button {
        width: 64px;
    }
</style>
