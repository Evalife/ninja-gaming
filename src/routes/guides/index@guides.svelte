<script context="module">
    // the function below takes context as an argument and it has a fetch method.
    // hence instead of saying fetch = context.fetch, we say { fetch }.
    // this is call destructuring
    export async function load({ fetch }) {
        const res = await fetch('https://jsonplaceholder.typicode.com/posts');
        const guides = await res.json();
        //console.log(guides);

        if(res.ok) {
            return {
                props: {
                    guides     //here, we use guides instead of guides: guides
                }
            }
        }

        return {
            status: res.status,
            error: new Error('Could not fetch the guides')
        }
    }
</script>

<script>
    export let guides;
</script>

<div class="guides">
    <ul>
        {#each guides as guide}
            <li>
                <a sveltekit:prefetch href={`/guides/${guide.id}`}>{guide.title}</a>
            </li>
        {/each}
    </ul>
</div>

<style>
    .guides {
        margin-top: 20px;
    }
    ul {
        list-style-type: none;
        padding: 0;
    }
    a {
        display: inline-block;
        margin-top: 10px;
        padding: 10px;
        border: 1px dotted rgba(255, 255, 255, 0.2);
    }
</style>