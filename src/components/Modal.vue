<template>
    <transition name="modal-fade">
        <div class="modal">
            <div class="modal__background" @click.prevent="close" />
            <div class="modal__content">
                <div class="modal__header header">
                    <slot name="header">
                        <div class="header__tick">&#10004;</div>
                        <h3 class="header__title">{{ title }}</h3>
                    </slot>
                </div>
                <div class="modal__body">
                    <slot name="body">
                        <p>
                            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean luctus, ipsum eu blandit lacinia, 
                            urna justo fringilla arcu, id elementum eros libero at odio. In placerat ex ut consequat luctus. 
                            Donec consectetur est pulvinar ante ullamcorper, eget cursus nisi lobortis.
                        </p>
                    </slot>
                </div>
                <div class="modal__footer"> 
                    <div class="modal__controls">
                        <button @click.prevent="close" class="button button__hollow">Cancel</button>
                        <button @click.prevent="close" class="button button__full">Continue</button>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        name: 'modal',

        props: {
            title: {
                type: String,
                default: 'Congratulations your jet2 holiday booking has been confirmed',
            },
        },

        methods: {
            close() {
                this.$emit("close");
            }
        },
    }
</script>

<style lang="scss" scoped>
    $primary: #203240;

    .modal {
        overflow-x: hidden;
        overflow-y: auto;
        position: fixed;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        z-index: 9;
    }

    .modal__background {
        background-color: #636f79;
        position: fixed;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        z-index: 1;
    }

    .modal__content {
        position: absolute;
        margin: 100px auto;
        background-color: #f2f2f2;
        z-index: 2;
        max-width: 550px;
        display: block;
        left: 0;
        right: 0;
    }

    .modal__header,
    .modal__body,
    .modal__footer {
        padding: 0 20px;
        margin: 0 auto;
    }

    .modal__header {
        font-weight: 700;
        text-align: left;
        display: flex;
        justify-content: space-between;
        flex-wrap: nowrap;
        margin-top: 15px;
        max-width: 400px;

        .header__title {
            font-size: 18px;
            display: block;
            flex-grow: 1;
            margin-bottom: 0;
        }

        .header__tick {
            margin-top: 15px;
            margin-right: 10px;
            flex-shrink: 0;
            width: 25px;
            height: 25px;
            display: block;
            border-radius: 50px;
            background-color: green;
            text-align: center;
            font-weight: 300;
            color: #ffffff;
            line-height: 25px;
        }
    }

    .modal__body {
        text-align: left;
        border-bottom: 1px solid;
        margin-bottom: 20px;
        display: flex;
        justify-content: center;

        p {
            font-size: 14px;
            max-width: 400px;
        }
    }

    .modal__footer {
        margin-bottom: 20px;
    }

    .modal__controls {
        display: flex;
        flex-direction: column;
        max-width: 400px;
        margin: 0 auto;

        @media (min-width: 560px) {
            flex-direction: row;
            justify-content: space-between;
        }
    }

    .button {
        display: block;
        margin: 0 auto;
        border-radius: 4px;
        height: 40px;
        font-size: 18px;
        width: 100%;
        font-weight: 700;
        margin-bottom: 5px;
        font-style: italic;

        @media (min-width: 560px) {
            display: inline-block;
            width: calc(50% - 5px);
        }

        &__full {
            border: 1px solid $primary;
            background-color: $primary;
            color: #ffffff;
        }

        &__hollow {
            border: 1px solid $primary;
            color: $primary;
            background-color: transparent;
        }
    }
</style>
