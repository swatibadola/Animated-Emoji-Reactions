# Animated-Emoji-Reactions
Created a set of animated emoji reactions one similar to you see in Google Meet using JavaScript.

## functionality Of Code
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
