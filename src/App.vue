<template>
    <div id="app">
        <h1>Modal Technical Test</h1>
        <h3>Martyn Taylor Gosling</h3>
        <div class="counter">
            <span class="counter__value">Modals Opened: {{ modalCount }} </span>
        </div>
        <button 
            @click.prevent="showModal('modal1Visible')"
            class="button button__open">
            Show Modal
        </button>
        <button 
            @click.prevent="showModal('modal2Visible')" 
            class="button button__open">
            Show Additional Modal
        </button>
        <modal v-show="modal1Visible" @close="hideModal('modal1Visible')" />
        <modal v-show="modal2Visible" @close="hideModal('modal2Visible')" :title="alternateTitle">
            <template v-slot:body>
                <p>
                    This is an additional modal with content that can be different than the base modal. 
                    You have opened {{ modalCount }} {{ countLabel }}!
                </p>
            </template>
        </modal>
    </div>
</template>

<script>
    import Modal from './components/Modal.vue'

    export default {
        name: 'App',
        
        components: {
            Modal,
        },

        data() {
            return {
                modal1Visible: false,
                modal2Visible: false, 
                modalCount: 0,
                alternateTitle: "Congratulations you have opened a second modal on the same page"
            };
        },

        computed: {
            /**
             * updates text when more than one modal has been opened
             */
            countLabel() {
                if (this.modalCount > 1) {
                    return 'modals';
                }

                return 'modal';
            }
        },

        methods: {
            /**
             * Show a modal with a given id
             */
            showModal(prop) {
                this[prop] = true;
                this.modalCount++;
            },

            /**
             * Hide a modal with a given id
             */
            hideModal(prop) {
                this[prop] = false;
            }
        }
    }
</script>

<style lang="scss">
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    .counter {
        margin-bottom: 10px;
    }

    .button {
        cursor: pointer; 

        &__open {
            display: block;
            margin: 0 auto 10px;
            height: 40px;
            width: 200px;
            border: 1px solid #203240;
            color: #203240;
            background-color: transparent;
            font-weight: 700;
        }
    }

    p {
        font-size: 14px;
        max-width: 400px;
        display: block;
    }
</style>

