<script lang="ts">
    import supabase from "$lib/supabase";
    import {readable, get} from 'svelte/store';
    let titleF: string = '';
    let contentF: string = '';
    import Photo from  './Photo.png';/**post.user.photo*/
    import './BlogPage.css';
    
    async function Login(e: Event) {
        window.location.href = '/SignupPage';
    };

    const posts = readable<null | any[]>(null, (set) => {
        supabase
            .from('posts')
            .select('*')
            .then(({ error, data }: { error: any, data: any[] | null }) => set(data))

            // const subscription = supabase
            //     .from('posts')
            //     .on('*', 
            //         (payload) => {
            //             const eventType = payload.eventType;
            //             const newRecord = payload.new;
            //             const oldRecord = payload.old;// payload.eventType
            //             // payload.new
            //             // payload.old
            //             if (eventType === 'INSERT') {
            //                 set([...(get(posts) ?? []), newRecord]);
            //             }

            //         })
            //     .subscribe();

            // return () => supabase.removeSubscription(subscription);
    });

    // Function to calculate the time difference and return a formatted string
    function getTimeAgo(timestamp: string): string {
        const currentDate = new Date();
        const postDate = new Date(timestamp);
        const timeDiff = currentDate.getTime() - postDate.getTime();

        const seconds = Math.floor(timeDiff / 1000);
        const minutes = Math.floor(seconds / 60);
        const hours = Math.floor(minutes / 60);
        const days = Math.floor(hours / 24);

        if (days > 0) {
        return `${days} day${days === 1 ? '' : 's'} ago`;
        } else if (hours > 0) {
        return `${hours} hour${hours === 1 ? '' : 's'} ago`;
        } else if (minutes > 0) {
        return `${minutes} minute${minutes === 1 ? '' : 's'} ago`;
        } else {
        return `${seconds} second${seconds === 1 ? '' : 's'} ago`;
        }
    }

</script>

<svelte:head>
	<title>Blog</title>
</svelte:head>

<main>
    <div id='column1'>
        <div class='column1Item'>
            <h1>Book crossing</h1>
        </div>
        <div class='column1Item'>
            Flowers
        </div>
        <div class='column1Item'>
            Dreams
        </div>
    </div>

    <div id='column2'>
        <div class='column2Item'>
            <form on:submit|preventDefault={Login} class='column2ItemWindow'>
                <input placeholder="Your nickname" readonly>
                <textarea placeholder="Type something" readonly></textarea>
                <button>Log in/sign up to post</button>
            </form>
        </div>
        
        <div class='column2Posts'>
            {#if $posts !== null}
              {#each $posts as post}
                <div id="Post">
                    <div class="PostHeader">
                        <!-- svelte-ignore a11y-img-redundant-alt -->
                        <img src={Photo} alt="User Photo" class="UserPhoto" />
                        <div class="NameHeader">
                            <h3 id="NickName">{post.title}</h3>
                            <p id="Time">Posted {getTimeAgo(post.created_at)}</p>
                        </div>
                    </div>
                  <p id="ScrollContent">{post.content}</p>
                </div>
              {/each}
            {:else}
              <p>Loading..</p>
            {/if}
        </div>
          
    </div>

    <div id='column3'>
        <div class='column1Item'>
            <h1>Book crossing</h1>
        </div>
        <div class='column1Item'>
            Flowers
        </div>
        <div class='column1Item'>
            Dreams
        </div>
    </div>
</main>