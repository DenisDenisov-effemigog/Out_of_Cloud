<template>
    <div class="modal">
        <div class="modal__bg"></div>
        <div class="modal__main">
            <div class="modal__close-btn" @click="closeModal">
                <img src="../assets/icons/close.svg" alt="">
            </div>
            <div class="modal__content">
                <div class="modal__title">Модальное окно</div>
                <form v-if="!answerFlag" action="" @submit.prevent="sendMail" class="modal__form">
                    <label for="" class="modal__label">
                        <input type="text" 
                            @focus="focusFlag = true"
                            @blur="focusFlag = false"
                            class="modal__input"
                            :class="{'modal__input--error': errorFlag || emailReg}"
                            name="email"
                            autocomplete="email"
                            autocorrect="off"
                            autocapitalize="off"
                            v-model="email"
                            @input="inputMail"
                        >
                        <span class="modal__label-text"
                            :class="{'modal__label-text--up': focusFlag || email.length > 0}">E-mail</span>
                        <div class="modal__label-icon"
                            v-show="email.length > 0"
                            @click="email = ''"
                        >
                            <img src="../assets/icons/close.svg" alt="">
                        </div>
                        <div class="modal__error-text modal__error-text--invalid"
                            v-show="!errorFlag && emailReg">Неверный формат почты</div>
                        <div ref="emailError" class="modal__error-text modal__error-text--invalid"
                            v-show="errorFlag">Поле не заполнено</div>
                    </label>
                    <button type="submit" class="modal__btn">Отправить</button>
                </form>
                <div v-else class="modal__answer">
                    <div class="modal__answer-text">
                        Мы свяжемся с Вами в ближайшее время
                    </div>
                    <button type="button" @click="closeModal" class="modal__btn">Закрыть</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"modal",
    data(){
        return{
            errorFlag: false,
            emailReg: false,
            email:'',
            focusFlag: false,
            answerFlag: false
        }
    },
    methods:{
        inputMail(){
            this.emailReg = false
            this.errorFlag = false
        },
        async sendMail(){
            if(this.email.length === 0){
                this.errorFlag = true
            }else if(!this.validateEmail(this.email)){
                this.emailReg = true
            }else{
                fetch('', {
                    method:"POST",
                    headers: {
                        'Content-Type': 'application/json;charset=utf-8'
                    },
                    body: this.email
                })
                    .then((response) => console.log(response))
                    .catch((error) => console.error("error " + error))
                this.answerFlag = true
                console.log(this.email);
            }
        },
        validateEmail(email){
            if(email.length > 0){
                let re = /\S+@\S+\.\S+/;
                return re.test(email);
            }
        },
        closeModal(){
            this.email = ''
            this.emailReg = false
            this.errorFlag = false
            this.answerFlag = false
            this.$emit("closeModal")
        }
    }
}
</script>