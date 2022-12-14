<script>
    export let postsArray;
    export let params;
    import { deletemessage } from "./components/script";
    console.log(postsArray);
</script>
{#await postsArray}
    <p>Loading..</p>
{:then postsArray} 
    {#each postsArray.msg as msgp}   
        {#if postsArray.token == msgp.userid || postsArray.roles =='635eb25438b20b702d8adfc9' || postsArray.roles =='635eb25438b20b702d8adfc8'}
        <div style="margin: 20px 0;width: 600px;height: auto;padding: 10px;border: 1px solid #389d77;border-radius: 6px;" id={msgp.messageid}>
            <p style="display: flex;justify-content: space-between;padding-bottom: 6px;border-bottom: 1px solid #a5a5a5;">
              <span>
                {msgp.user}
                <span style="font-size: 0.8rem;">#{msgp.messageid}</span>
              </span>
              <span>
                <a href="/" on:click={deletemessage(msgp.messageid,params)} onclick="return false" style="padding: 0 8px;color: #f9f9f9;border-radius: 5px;background-color: #b4241c;margin: 0 5px;">x</a>
                {msgp.datetime}</span>
            </p>
            <p style="margin: 6px;word-wrap: break-word;" id="text-area{msgp.messageid}">{msgp.message}</p>
          </div>
        {:else}
        <div style="margin: 20px 0;width: 600px;height: auto;padding: 10px;border: 1px solid #389d77;border-radius: 6px;" id={msgp.messageid}>
            <p style="display: flex;justify-content: space-between;padding-bottom: 6px;border-bottom: 1px solid #a5a5a5;">
              <span>
                {msgp.user}
                <span style="font-size: 0.8rem;">#{msgp.messageid}</span>
              </span>
              <span>{msgp.datetime}</span>
            </p>
            <p style="margin: 6px;word-wrap: break-word;" id="text-area{msgp.messageid}">{msgp.message}</p>
          </div>
        {/if}
    {/each}
{/await}