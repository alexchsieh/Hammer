<script>
// local functions can be decalred here
export default {
    props: {
        // properties go here
        // ex: title: String,
        timeSince: String,
        poster: String,
        children: Array,
        comment: String,
        cid: String,

        // threads
        parentId: String,
        parentComment: String,
    },
    data() {
        return {
            // responsive variables go here
            // ex: count: 0,
        }
    },
    methods: {
        // callable functions for HTML go here
        // ex: incCount()
        // {
        //     this.count++;
        // }
        getHref(a)
        {
            return ('#'+a);
        },
        removeBlinks()
        {
            document.querySelectorAll('.blink').forEach(function(element) {
                element.classList.remove('blink');
                // alert('try unblink');
            });

        },
        animateComment(pid)
        {
            // alert("test");
            this.removeBlinks();
            
            let parent = document.getElementById(pid);
            setTimeout(function() {
                parent.classList.add("blink");
            }, 10);
        },
    },
    mounted()
    {
        let wrapper = document.getElementById('displayCommentBox');
        wrapper.scrollTop = wrapper.scrollHeight;
    }
}
</script>
<template>
    <!-- HTML for components goes here -->
    <div class="displayedComment">
        <!-- <p>parentId: <strong> {{parentId}} </strong></p>
        <p>parentComment <strong> {{parentComment}} </strong></p>
        <p class="commentOwner">Username: <strong>{{ poster }}</strong></p>
        <p>timestamp: <strong>{{ timestamp }}</strong></p>
         -->
         <span class="userPoster">
            <img width="15" src="../assets/tempAvatar.png"/>
            <p class="userName">{{ poster }}</p>
         </span>
        <a class="repliedComment" :href="getHref(parentId)" v-if="parentId != null" @click="animateComment(parentId)"><strong>Reply to:</strong>{{parentComment}} ...</a>
        <p class="ActualComment">{{ comment }}</p>
        <p class="timeSince">{{ timeSince }}</p>
        <!-- <p>commentID: <strong>{{cid}}</strong></p> -->
    </div>
</template>
<style scoped>
/* Styles for component go here */
.displayedComment {
    padding: 10px;
    width: calc(100% - 24px);
    border-radius: 10px 5px 5px 15px;
    margin-bottom: 2px;
    /* border: 2px solid; */
    box-shadow: 1px 1px 3px rgb(0, 0, 0);
    background-color: rgb(236, 255, 221);

}
.repliedComment
{
    border-left: 4px solid rgb(183, 183, 183);
    padding-left: 4px;
    line-height: 25px;
    color: rgb(114, 114, 114);
}
.userName
{
    /* vertical-align: center;
    background-color: blue; */
    vertical-align: middle;
}
.userPoster
{
    /* background-color: red; */
    display: flex;
    margin-bottom: 10px;
    vertical-align: center;
}

.ActualComment
{
    margin: 0 4px;
}
.timeSince
{
    margin-top: 5px;
    color: grey;
    margin-left: 10px;
    font-size: 11px;
}
strong{
    font-weight: bold;
}
</style>