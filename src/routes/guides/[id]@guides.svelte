<script context="module">
    export async function load({ fetch, params }) {  // the load fn also receives the page parameter

        const id = params.id;  //"id" here must tally with file name.if file name = [abc].svelte, then this should be page.params.abc.
        
        const res = await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`);
        const guide = await res.json();

        if (res.ok) {
            return {
                props: {
                    guide, //here, we use guides instead of guides: guides
                },
            };
        }

        return {
            status: 301,
            //error: new Error("Could not fetch the guides"),
            redirect: '/guides'
        };

    }
</script>

<script>
    export let guide;
</script>

<div class="guide">
    <h2>{guide.title}</h2>
    <p>{guide.body}</p>
</div>

<style>
    .guide {
        margin-top: 40px;
        padding: 10px;
        border: 1px dotted rgba(255, 255, 255, 0.2);
    }
</style>
