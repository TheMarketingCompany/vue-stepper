<template>
    <div style="padding: 2rem 3rem; text-align: left;">
        <div class="answer1" @click="userMadeSelection(1)">
            Antwort 1
        </div>
        <div class="answer2" @click="userMadeSelection(2)">
            Antwort 2
        </div>
        <div class="answer3" @click="userMadeSelection(3)">
            Antwort 3
        </div>
        <div class="answer4" @click="userMadeSelection(4)">
            Antwort 4
        </div>
    </div>
</template>

<script>
    import {validationMixin} from 'vuelidate'
    import {required, email} from 'vuelidate/lib/validators'

    export default {
        props: ['clickedNext', 'currentStep'],
        mixins: [validationMixin],
        data() {
            return {
                form: {
                    username: '',
                    demoEmail: '',
                    message: ''
                }
            }
        },
        validations: {
            form: {
                username: {
                    required
                },
                demoEmail: {
                    required,
                    email
                },
                message: {
                    required
                }
            }
        },
        methods : {
            userMadeSelection(answer) {
                console.log("hello world " + answer);
                this.$emit('can-continue', {value: true});
                this.$parent.nextStep();
            }
        },
        mounted() {
            if(!this.$v.$invalid) {
                this.$emit('can-continue', {value: true});
            } else {
                this.$emit('can-continue', {value: false});
            }
        }
    }
</script>
