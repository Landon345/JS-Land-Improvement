<script lang="ts">
  import emailjs from "@emailjs/browser";
  const randomNumber1 = Math.floor(Math.random() * 20);
  const randomNumber2 = Math.floor(Math.random() * 20);
  let answer;
  let name = "";
  let sendingEmail = false;
  $: showEmailSuccess = false;
  $: showEmailFailed = false;

  const sendEmail = async (e) => {
    answer = "";
    sendingEmail = true;
    try {
      const result = await emailjs.sendForm(
        import.meta.env.VITE_EMAILJS_SERVICE_ID,
        import.meta.env.VITE_EMAILJS_TEMPLATE_ID,
        e.target,
        import.meta.env.VITE_EMAILJS_PUBLIC_KEY
      );
      console.log("SUCCESS!", result.text);
      showEmailSuccess = true;
      sendingEmail = false;
      setTimeout(() => {
        showEmailSuccess = false;
      }, 5000);
    } catch (error) {
      answer = "";
      console.log("FAILED...", error.text);
      showEmailFailed = true;
      sendingEmail = false;
      setTimeout(() => {
        showEmailFailed = false;
      }, 5000);
    }
  };
</script>

<div class="contact-container">
  <div class="inner-contact-container">
    <div class="reach-here">
      <h3 class="contact-header">CONTACT US</h3>
      <p>701-347-1545</p>
      <p>team@jslandimprovement.com</p>
      <a
        class="facebook-link"
        href="https://www.facebook.com/JSLandImprovement"
        target="_blank"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          data-name="Layer 1"
          viewBox="0 0 24 24"
          id="facebook"
          width="30"
          height="30"
          fill="#fff"
          ><path
            d="M15.12,5.32H17V2.14A26.11,26.11,0,0,0,14.26,2C11.54,2,9.68,3.66,9.68,6.7V9.32H6.61v3.56H9.68V22h3.68V12.88h3.06l.46-3.56H13.36V7.05C13.36,6,13.64,5.32,15.12,5.32Z"
          ></path></svg
        >
      </a>
    </div>
    <form on:submit|preventDefault="{sendEmail}">
      {#if showEmailSuccess || showEmailFailed}
        {#if showEmailSuccess}
          <div class="alert success">
            <p>Message sent successfully!</p>
          </div>
        {/if}
        {#if showEmailFailed}
          <div class="alert error">
            <p>Message failed to send. Please try again.</p>
          </div>
        {/if}
      {:else if sendingEmail}
        <div class="alert neutral">
          <p>Sending Message...</p>
        </div>
      {:else}
        <div class="alert hidden">
          <p>Message status</p>
        </div>
      {/if}
      <div class="inputs">
        <div class="name-phone">
          <input
            type="text"
            required
            name="name"
            placeholder="Name"
            class="input-box"
            bind:value="{name}"
          />
          <input
            type="text"
            required
            name="phone"
            placeholder="Phone"
            class="input-box"
          />
        </div>
        <input
          type="email"
          required
          name="email"
          placeholder="Email"
          class="input-box"
        />
        <textarea
          name="message"
          class="textarea input-box"
          placeholder="Let us know what kind of project you have in mind or ask any questions you have!"
        ></textarea>
      </div>
      <div class="submit-container">
        <p class="math-problem">
          {randomNumber1} + {randomNumber2} =
        </p>
        <input class="answer" type="text" required bind:value="{answer}" />
        <input
          type="submit"
          value="Submit"
          class="submit-button"
          disabled="{randomNumber1 + randomNumber2 != answer || sendingEmail}"
        />
      </div>
    </form>
  </div>
</div>

<style>
  .contact-container {
    padding: 80px 0 20px 0;
    width: 100%;
    border-top: 1px solid #222;
    background-color: #f7f7f7;
  }
  .inner-contact-container {
    display: flex;
    flex-direction: column;
    width: 90%;
    margin: auto;
  }
  .contact-header {
    font-size: 20px;
    text-transform: uppercase;
    margin-bottom: 30px;
  }
  p {
    font-size: 15px;
    margin-bottom: 10px;
  }
  .facebook-link {
    display: flex;
    align-items: center;
    margin: 30px 0 8px 0;
    background-color: #3b5998;
    transition: linear 0.2s all;
    width: min-content;
    border-radius: 4px;
    padding: 8px;
  }
  .facebook-link:hover {
    background-color: #294d9a;
  }
  form {
    display: flex;
    flex-direction: column;
    width: 100%;
  }
  form p {
    padding: 0;
    margin: 0;
  }
  .alert {
    padding: 20px;
    margin-bottom: 10px;
    margin: 0 10px;
    border-radius: 4px;
  }
  .success {
    background-color: #d4edda;
    color: #155724;
  }
  .error {
    background-color: #f8d7da;
    color: #721c24;
  }
  .hidden {
    background-color: #f5f5f5;
    color: #f5f5f5;
  }
  .neutral {
    background-color: #fff;
    color: #222;
  }
  .inputs {
    display: flex;
    flex-direction: column;
    width: 100%;
  }

  form input {
    margin-bottom: 10px;
    border: 2px solid #222;
    padding: 20px;
    font-size: 16px;
  }
  form input::placeholder {
    color: #222;
  }
  .submit-button {
    background-color: #ffc801;
    color: #222;
    text-transform: uppercase;
    font-weight: 600;
    border: none;
    padding: 22px;
    transition: linear 0.2s all;
    width: min-content;
    cursor: pointer;
    letter-spacing: 2px;
  }
  .submit-button:hover {
    background-color: #be963e;
  }
  .submit-button:disabled {
    background-color: #ccc;
    color: #666;
    cursor: not-allowed;
  }
  .submit-container {
    display: flex;
    justify-content: flex-end;
    width: 100%;
    align-items: center;
  }
  .textarea {
    height: 100px;
    margin-bottom: 10px;
    padding: 8px;
    border: 2px solid #222;
    padding: 20px;
    font-family: "montserrat", "sans-serif";
    font-size: 16px;
    color: #222;
    font-weight: 500;
  }
  .textarea::placeholder {
    color: #222;
    font-family: "montserrat", "sans-serif";
    font-weight: 500;
  }
  .math-problem {
    font-size: 16px;
    margin-right: 10px;
    color: #666;
  }
  .answer {
    width: 50px;
    padding: 20px 5px;
    margin-right: 24px;
  }
  .name-phone {
    display: flex;
    flex-direction: column;
  }
  @media (min-width: 1200px) {
    .contact-container {
      padding: 10px 0 20px 0;
    }
    .inner-contact-container {
      display: grid;
      grid-template-columns: 1fr 3fr;
      justify-items: center;
    }
    .reach-here {
      margin-top: 70px;
      margin-right: 40px;
    }
    .name-phone {
      display: grid;
      grid-template-columns: 1fr 1fr;
    }
    .input-box {
      margin: 10px;
    }
    .contact-header {
      font-size: 42px;
    }
  }
</style>
