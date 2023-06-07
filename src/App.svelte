<div class="flexy">
    <div class="bottom-app-bar-container flexor">
        <div class="flexor-content">
            <h5>Right FAB</h5>

            <img
                    alt="Page content placeholder"
                    src="/page-content.jpg"
                    style="display: block; max-width: 100%; height: auto; margin: 1em auto;"
            />
        </div>

        <BottomAppBar
                variant="static"
                color={secondaryColor ? 'secondary' : 'primary'}
        >
            <Section>
                <IconButton class="material-icons" aria-label="Search">
                    settings
                </IconButton
                >
                <IconButton class="material-icons" aria-label="Search"
                >person
                </IconButton
                >
                <IconButton class="material-icons" aria-label="Search"
                >center_focus_weak
                </IconButton
                >
                <IconButton class="material-icons" aria-label="Search"
                >car_repair
                </IconButton
                >
                <IconButton class="material-icons" aria-label="More"
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

    let secondaryColor = false;
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