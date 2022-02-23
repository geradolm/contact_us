<script>
    import { fade } from "svelte/transition";
    let fields = { email: "", name: "", subject: "", message: "" };
    let error = false;
    let isSuccess = false;
    let hasBeenClicked = false;

    function validateEmail(email) {
        const emailRegEx =
            /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        return emailRegEx.test(String(email).toLowerCase());
    }

    const errorMessage = "All the fields are mandatory";

    function submitHandler(e) {
        isSuccess = true;
        setTimeout(function () {
            isSuccess = false;
        }, 2000);
        fields = {};
    }
    function handleSubmission() {
        hasBeenClicked = true;
    }
</script>

<main>
    <div class="page">
        <div class="header">
            <h2>Contact Us</h2>
            <p>
                If you would like to get in touch with us, please use the
                contact form.
            </p>
        </div>

        <div class="container">
            <div class="top">
                <p>
                    {#if error == true}
                        <p class="alert">{errorMessage}</p>
                    {:else if isSuccess}
                        <p class="alert" transition:fade={{ duration: 150 }}>
                            Message Sent
                        </p>
                    {/if}
                </p>
            </div>
            <form id="contactForm" on:submit|preventDefault={submitHandler}>
                <label class="mb-0" for="email">Email: </label>
                <input
                    type="email"
                    id="email"
                    bind:value={fields.email}
                    required
                />
                <label class="mb-0" for="name">Name: </label>
                <input
                    type="text"
                    id="name"
                    bind:value={fields.name}
                    required
                />
                <label class="mb-0" for="subject">Subject: </label>
                <input
                    type="text"
                    id="subject"
                    bind:value={fields.subject}
                    required
                />
                <label class="mb-0" for="message">Message: </label>
                <input
                    type="text"
                    id="message"
                    bind:value={fields.message}
                    required
                />
                <button
                    type="submit"
                    class="button-submit"
                    on:click={handleSubmission}>SEND</button
                >
            </form>
        </div>
    </div>
</main>

<style>
    main {
        align-items: center;
        background-size: cover;
        display: flex;
        flex-direction: column;
        font-family: "Poppins", sans-serif;
        font-size: 16px;
        margin: 0;
        padding: 0;
        text-align: center;
    }

    .page {
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        height: 100%;
        max-width: 1440px;
        min-width: 350px;
        padding: 1rem 1rem;
        width: 100%;
    }

    .header h2 {
        color: #ffffff;
        font-size: 40px;
        font-weight: 600;
        line-height: 3rem;
        margin-top: 0rem;
    }

    .header p {
        color: #ffffff;
        font-size: 16px;
        font-weight: 400;
        line-height: 1.5rem;
        margin-bottom: 0px;
    }

    .top p {
        color: rgb(255, 255, 255);
        font-family: "Poppins", sans-serif;
        font-size: 1.59rem;
        font-weight: 400;
        margin: 0;
        padding-left: 0px;
        padding-right: 0px;
    }

    .mb-0 {
        padding-right: 400px;
    }

    form {
        align-items: center;
        background: white;
        border-radius: 0.5rem;
        box-shadow: 0px 7px 2px 0px;
        color: #000000;
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        margin: 2rem 0;
    }

    input {
        border: 2px solid rgb(0, 0, 0);
        border-radius: 0.2rem;
        box-sizing: border-box;
        font-family: "Poppins", sans-serif;
        font-weight: 600;
        height: 3rem;
        margin-top: 0.25rem;
        margin-bottom: 1.75rem;
        padding-left: 1rem;
        width: 85%;
    }

    .button-submit {
        padding-top: 8px;
        padding-bottom: 8px;
        border: none;
        box-shadow: 0px 1px 1px 2px;
        font-size: 16px;
        box-sizing: border-box;
        color: rgb(37, 25, 25);
        cursor: pointer;
        font-weight: 500;
        letter-spacing: 1px;
        width: 50%;
    }

    @media screen and (min-width: 720px) {
        main {
            background-clip: border-box;
            background-repeat: repeat;
            background-size: auto 50rem;
        }

        .page {
            align-items: center;
            flex-direction: row;
            height: 100vh;
            justify-content: center;
        }

        .header {
            max-width: 30rem;
            padding-right: 1rem;
            text-align: left;
            width: 49%;
        }

        .container {
            align-items: flex-start;
            max-width: 35rem;
            width: 49%;
        }

        form {
            padding: 1rem 0;
        }
    }
</style>
