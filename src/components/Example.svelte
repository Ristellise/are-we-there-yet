<script>
    import AllDone from '$components/AllDone.svelte';
    import Error from '$components/Error.svelte';
    import Show from '$components/Show.svelte';
    import Position from '$components/Position.svelte';
    import { createLocalization } from '$components/Lang';
    import Localized from '$components/Lang/Localized.svelte';
    import { getContext } from 'svelte';

    const lang = getContext('lang');

    export let accent;

    const two_hours = 2 * 60 * 60 * 1000;
    const two_hours_ago = new Date(new Date().getTime() - two_hours);
    const in_two_hours = new Date(new Date().getTime() + two_hours);

    const positions = [
        {
            id: 1,
            name: 'Translation',
            acronym: 'TL',
        },
        {
            id: 2,
            name: 'Translator Check',
            acronym: 'TLC',
        },
        {
            id: 3,
            name: 'Encode',
            acronym: 'ENC',
        },
        {
            id: 4,
            name: 'Editing',
            acronym: 'ED',
        },
        {
            id: 5,
            name: 'Timing',
            acronym: 'TM',
        },
        {
            id: 6,
            name: 'Typesetting',
            acronym: 'TS',
        },
        {
            id: 7,
            name: 'Quality Control',
            acronym: 'QC',
        },
        {
            id: 8,
            name: 'Custom Position Example',
            acronym: 'KFX',
        },
    ];
    $: localize = createLocalization($lang).localize;
    $: exampleShow = {
        id: 1,
        name: 'The Wonderful Life of Furballs',
        status: localize('EXAMPLE_STATUS'),
        progress: 'Airing',
        created_at: two_hours_ago.toISOString(),
        updated_at: two_hours_ago.toISOString(),
        poster: 'https://placekitten.com/460/646',
        joint_groups: [
            {
                id: 1,
                name: 'Meow Subs',
                acronym: 'MS',
                icon: 'https://placekitten.com/200/200',
                shows: [],
            },
        ],
        episodes: [
            {
                id: 1,
                number: 1,
                air_date: two_hours_ago.toISOString(),
                season: 'Fall 2020',
                release: false,
                updated_at: two_hours_ago.toISOString(),
                staff: [
                    {
                        id: 1,
                        finished: false,
                        updated_at: two_hours_ago.toISOString(),
                        position: {
                            id: 1,
                            name: 'Translation',
                            acronym: 'TL',
                        },
                        member: {
                            id: -1,
                            name: 'Redacted',
                            group: 1,
                        },
                    },
                    {
                        id: 2,
                        finished: true,
                        updated_at: two_hours_ago.toISOString(),
                        position: {
                            id: 2,
                            name: 'Encode',
                            acronym: 'ENC',
                        },
                        member: {
                            id: -1,
                            name: 'Redacted',
                            group: 1,
                        },
                    },
                ],
            },
            {
                id: 2,
                number: 2,
                air_date: two_hours_ago.toISOString(),
                season: 'Fall 2020',
                release: false,
                updated_at: two_hours_ago.toISOString(),
                staff: [
                    {
                        id: 1,
                        finished: false,
                        updated_at: two_hours_ago.toISOString(),
                        position: {
                            id: 1,
                            name: 'Translation',
                            acronym: 'TL',
                        },
                        member: {
                            id: -1,
                            name: 'Redacted',
                            group: 1,
                        },
                    },
                    {
                        id: 2,
                        finished: false,
                        updated_at: two_hours_ago.toISOString(),
                        position: {
                            id: 2,
                            name: 'Encode',
                            acronym: 'ENC',
                        },
                        member: {
                            id: -1,
                            name: 'Redacted',
                            group: 1,
                        },
                    },
                ],
            },
            {
                id: 3,
                number: 3,
                air_date: in_two_hours.toISOString(),
                season: 'Fall 2020',
                release: false,
                updated_at: two_hours_ago.toISOString(),
                staff: [
                    {
                        id: 1,
                        finished: false,
                        updated_at: two_hours_ago.toISOString(),
                        position: {
                            id: 1,
                            name: 'Translation',
                            acronym: 'TL',
                        },
                        member: {
                            id: -1,
                            name: 'Redacted',
                            group: 1,
                        },
                    },
                    {
                        id: 2,
                        finished: false,
                        updated_at: two_hours_ago.toISOString(),
                        position: {
                            id: 2,
                            name: 'Encode',
                            acronym: 'ENC',
                        },
                        member: {
                            id: -1,
                            name: 'Redacted',
                            group: 1,
                        },
                    },
                ],
            },
        ],
    };
</script>

<div class="app-example grid grid-cols-1 gap-2 m-auto">
    <Show show={exampleShow} {accent} />
    <Error message={localize('EXAMPLE_ERROR')} />
    <AllDone />
    <div>
        <div class="rounded shadow-md px-4 py-4 bg-white dark:bg-gray-700">
            <h3 class="text-center text-xl pb-3">
                <Localized key="ALL_POSITIONS" />
            </h3>
            <div class="flex gap-1 justify-center text-sm">
                {#each positions as position (position.id)}
                    <Position {position} />
                {/each}
            </div>
        </div>
    </div>
</div>

<style>
    .app-example {
        width: 27.5rem;
    }
</style>
