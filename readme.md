# Animated-Emoji-Reactions
I developed a collection of animated emoji reactions, similar to the ones you encounter in Google Meet, using JavaScript.

# Notes

## functionality js
``` 
class EmojiAnimate {
    constructor() {
        this.emojis = document.querySelectorAll(".emoji-list button");
        this.container = document.querySelector(".emoji-container");
        this.handleEmojiClick = this.handleEmojiClick.bind(this);
        this.addEventListeners()
    }

    addEventListeners() {
        this.emojis.forEach((emoji) =>
            emoji.addEventListener("click", this.handleEmojiClick)
        )

        setTimeout(() => {
            this.emojis[7].click();
        }, 200);
        setTimeout(() => {
            this.emojis[1].click();
        }, 1000);
    }

    handleEmojiClick(e) {
        //Creating a new element to hold the emoji
        const emojiElement = document.createElement("div");
        emojiElement.classList.add("emoji-animate");

        // Get the emoji form the clicked element
        const { innerHTML } = e.target;
        emojiElement.innerHTML = innerHTML;

        // Placing the element inside the container
        this.container.appendChild(emojiElement);

        // Get positions
        const { height, left } = e.target.getBoundingClientRect();
        const { bottom, top, width } = this.container.getBoundingClientRect();

        //Animation
        const animation = emojiElement.animate(
            [
                {
                    opacity: 1,
                    transform: `translate(${left}px, ${bottom}px)`
                },
                {
                    opacity: 0,
                    transform: `translate(${width / 2}px, ${top - height}px)`
                },
            ],
            {
                duration: 2000,
                easing: "cubic-bezier(.47, .48,.44,.86)",
            }
        );
        console.log("ANIMATED")

        //Removing element once it has finished animating
        animation.onfinish = () => emojiElement.remove();
    }
}

new EmojiAnimate();
 ```

## style css
```
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

::selection{
    background: transparent;
}

body{
    background: #202124;
    display: grid;
    padding: 15px;
    gap: 15px;
}

.emoji-container{
    background: #2c2c2c;
    border-radius: 10px;
    height: calc(100dvh - 115px);
    overflow: hidden;
    position: relative;
}

.emoji-list{
    margin-inline: auto;   /* Brings content list to center */
    background: #2c2c2c;
    display: table;
    border-radius: 50px;
    padding: 10px;
}

.emoji-list ul{
    display: flex;  /* Aligns content list in a line */ 
}

.emoji-list ul li{
    display: flex;
    cursor: pointer;
    margin-inline: 2.5px;
}

.emoji-list ul li button{
    font-size: 2em; /* Makes the font-size 2 times the original font-size */ 
    cursor: pointer;
    padding: 2px;
    border: none;
    border-radius: 50%;
    background-color: transparent;
    outline-color: rgba(255,255,255,0.1);
    line-height: 44px;
}


.emoji-list ul li button:focus-visible{
    outline: 2px solid rgba(255,255,255,0.5);
    background: rgba(255,255,255,0.05);
}

.emoji-animate{
    font-size: 3em;
    will-change: transform;
    position: absolute;
}
```
