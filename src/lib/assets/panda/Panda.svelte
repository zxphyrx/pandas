<style lang="scss">
    .panda {
        background-color: rgb(42, 42, 42);
        padding: 36px;
        border-radius: 16px;
    }

    #message {
        text-align: center;
        width: 100vw;
        font-size: 1.5rem;
    }

    .buttons {
        display: flex;
        flex-direction: row;
        margin-top: 16px;

        button {
            background-color: white;
            font-size: 1.5rem;
            outline: none;
            border: none;
            padding: 4px;
            margin-right: 8px;
            border-radius: 8px;
            cursor: pointer;
        }
    }
</style>

<script>
    function randRange(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function handleClick(button) {
        path = button.paths[randRange(0, button.paths.length - 1)];
    }

    let paths = [
        {
            "message": "He just woke up!",
            "buttons": [
                {
                    "text": "Feed him",
                    "paths": [
                        {
                            "message": "He's not eating! You should probably leave him alone.",
                            "buttons": [
                                {
                                    "text": "Leave him alone",
                                    "paths": [
                                        {
                                            "message": "He goes back to sleep."
                                        }
                                    ]
                                },
                                {
                                    "text": "Tap on the glass",
                                    "paths": [
                                        {
                                            "message": "He growls angrily."
                                        }
                                    ]
                                }
                            ]
                        },
                        {
                            "message": "He eats the bamboo hungrily.",
                            "buttons": [
                                {
                                    "text": "Get closer",
                                    "paths": [
                                        {
                                            "message": "You lock eyes, and it's almost like he's smiling!"
                                        },
                                        {
                                            "message": "You lock eyes, and he growls at you."
                                        }
                                    ]
                                },
                                {
                                    "text": "Leave him alone to eat",
                                    "paths": [
                                        {
                                            "message": "He keeps eating!"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
    let path = $state(paths[randRange(0, paths.length - 1)]);
    let buttons = $derived(path.buttons);
</script>

<div class="section">
    <div class="panda">
        <img src="/panda.svg">
    </div>

    <p id="message">{path.message}</p>

    <div class="buttons">
        {#each buttons as button}
            <button onclick={() => { handleClick(button) }}>{button.text}</button>
        {/each}
    </div>

</div>