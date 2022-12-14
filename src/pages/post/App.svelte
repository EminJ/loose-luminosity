<script>
  import { onMount } from "svelte";
  import axios from "axios";
  import Message from "./message.svelte";
  import {
    gets,
    like,
    dislike,
    send_message,
    postsave,
  } from "./components/script";
  let params;
  let msgveriable;
  onMount(async () => {
    const urlSearchParams = new URLSearchParams(window.location.search);
    params = Object.fromEntries(urlSearchParams.entries()).id;
    gets(params);
    axios.post('https://191.101.1.221:5678/api/show/post/comments', {
        token:decodeURIComponent(document.cookie).split(';')[0].split('=')[1] || '',
        postid: params,
    })
    .then(function (response) {
        console.log(response.data);
        msgveriable=response.data;
    });
  });
  
</script>

<div class="outline">
  <div class="menu">
    <b id="post_name" />
    <div class="menualt">
      <span class="light" id="likecount" />
      <a href="/" on:click={like(params)} onclick="return false"
        ><i class="bx bx-like" id="like" /></a
      >
      <span class="light" id="dislikecount" />
      <a href="/" on:click={dislike(params)} onclick="return false"
        ><i class="bx bx-dislike" id="dislike" /></a
      >
      <a href="/" on:click={postsave(params)} onclick="return false"
        ><i class="bx bx-bookmark" id="comments" /></a
      >
    </div>
  </div>

  <div class="main" id="main" />

  <div class="alert" id="alertdel">
    <span class="closebtn" onclick="this.parentElement.style.display='';"
      >&times;</span
    >Yorumunuz Silinmiştir.
  </div>
  <div class="alert" id="alertedit" style="background-color:#cd8e12">
    <span class="closebtn" onclick="this.parentElement.style.display='';"
      >&times;</span
    >Yorumunuz Değiştirilmiştir.
  </div>
  <div class="alert" id="alertediterr1" style="background-color:#cd8e12">
    <span class="closebtn" onclick="this.parentElement.style.display='';"
      >&times;</span
    >Yorumunuz Değiştirilmedi. Bir değişiklik Yapılmadı!
  </div>

  <div class="comments">
    <input
      type="text"
      class="commentstext"
      id="sendcomments"
      placeholder="Yorum Yaz.."
    />

    <button class="commentsbtn" on:click={send_message(params)}>Gönder</button>
    <div id="show_comments">
      {#if msgveriable}
        <Message postsArray={msgveriable} params={params}/>
      {/if}
    </div>
  </div>
</div>

<style>
  @import "https://cdn.quilljs.com/1.3.6/quill.snow.css";
  #post_name {
    margin-right: 10px;
  }
  .alert {
    margin-top: 20px;
    padding: 20px;
    background-color: #f44336;
    color: white;
    display: none;
  }

  .closebtn {
    margin-left: 15px;
    color: white;
    font-weight: bold;
    float: right;
    font-size: 22px;
    line-height: 20px;
    cursor: pointer;
    transition: 0.3s;
  }

  .closebtn:hover {
    color: black;
  }
  .outline {
    width: 960px;
    margin: auto;
    padding: 0 30px;
  }
  .menu {
    height: auto;
    font-size: 1.2rem;
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  .menualt {
    font-size: 1.5rem;
    display: flex;
    flex-wrap: nowrap;
  }
  .main {
    font-size: 1.28rem;
    word-break: break-word;
  }
  .menu a {
    margin: 0 8px;
  }
  .comments {
    width: 100%;
    height: 500px;
    margin-top: 30px;
  }
  .light {
    font-size: 1rem;
    color: #a5a5a5;
  }
  .commentstext {
    width: 375px;
    padding-left: 5px;
    height: 25px;
    margin-left: 0;
    border: 1px solid #389d77;
    background-color: transparent;
    border-radius: 5px;
  }
  .commentsbtn {
    padding: 5px 10px;
    background-color: transparent;
    border: 1px solid #389d77;
    border-radius: 5px;
    transition: 0.25s;
  }
  .commentsbtn:hover {
    background-color: #389d77;
    color: #f9f9f9;
  }
  .bx-like:hover {
    color: #389d77;
    font-weight: bold;
  }
  .bx-dislike:hover {
    color: #b4241c;
    font-weight: bold;
  }
  .bx-bookmark:hover {
    color: #389d77;
    font-weight: bold;
  }
  @media screen and (max-width: 1080px) {
    .outline {
      width: 860px;
    }
  }
  @media screen and (max-width: 960px) {
    .outline {
      width: 750px;
    }
  }
  @media screen and (max-width: 820px) {
    .outline {
      width: 550px;
    }
    .message_outline {
      width: 460px;
    }
    .commentstext {
      width: 290px;
    }
  }
  @media screen and (max-width: 620px) {
    .outline {
      width: 480px;
    }
    .message_outline {
      width: 380px;
    }
    .commentstext {
      width: 200px;
    }
  }
  @media screen and (max-width: 540px) {
    .outline {
      width: 350px;
    }
    .message_outline {
      width: 320px;
    }
    .commentstext {
      width: 200px;
    }
    #likecount {
      display: none;
    }
    #dislikecount {
      display: none;
    }
  }
</style>
