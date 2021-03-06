<template>
    <div class="schedule-section-level-item-container">
        <div class="schedule-section-level-item-teacher-container">
            <img v-if="checkSmallPhoto(teacher)" class="schedule-section-level-item-teacher-photo" 
                 :src="teacher.smallPhoto" :alt="teacher.name">
            <img v-else class="schedule-section-level-item-teacher-photo" 
                 src="../assets/teachers/teacher-default-small.svg" alt="">
            <div class="schedule-section-level-item-teacher-info-container">
                <span v-if="checkName(teacher)" class="schedule-section-level-item-teacher-name">{{teacher.name}}</span>
                <span v-else class="schedule-section-level-item-teacher-name-empty">носитель</span>
                <span v-if="checkPosition(teacher)" class="schedule-section-level-item-teacher-post">{{teacher.position}}</span>
                <span v-else class="schedule-section-level-item-teacher-post-empty">преподаватель</span>
            </div>
        </div>
        <div class="schedule-section-level-item-time-info-container">
            <span class="schedule-section-level-item-time">{{timeString}}</span>
            <span class="schedule-section-level-item-days">{{days}}</span>
            <div class="schedule-section-level-item-signup-tablet">
                <div @click="showModal('signup-form-modal-tablet')" v-if="isAvailable" class="schedule-section-level-item-signup-container">
                    <span class="schedule-section-level-item-signup-title">Записаться</span>
                    <img class="schedule-section-level-item-signup-arrow-image" src="../assets/common/arrow.svg" alt="arrow"/>
                </div>
                <span v-else class="schedule-section-level-item-closed">набор закрыт</span>
            </div>
            <div class="schedule-section-level-item-signup-mobile">
                <div @click="showModal('signup-form-modal-phone')" v-if="isAvailable" class="schedule-section-level-item-signup-container">
                    <span class="schedule-section-level-item-signup-title">Записаться</span>
                    <img class="schedule-section-level-item-signup-arrow-image" src="../assets/common/arrow.svg" alt="arrow"/>
                </div>
                <span v-else class="schedule-section-level-item-closed">набор закрыт</span>
            </div>
        </div>
        <span class="schedule-section-level-item-start-date">{{startDate | moment("DD.MM.YYYY")}}</span>
        <div class="schedule-section-level-item-duration">{{duration}}</div>
        <div class="schedule-section-level-item-price-container">
            <div class="schedule-section-level-item-price-info-container">
            <span v-if="priceWithoutDiscount" class="schedule-section-level-item-price-without-discount">
                {{priceWithoutDiscount}}
                <span v-if="discountValue" class="schedule-section-level-item-discount">{{discountString}}</span>
            </span>
                <span class="schedule-section-level-item-price">{{price}}</span>
            </div>
            <div @click="showModal('signup-form-modal')" v-if="isAvailable" class="schedule-section-level-item-signup-container">
                <span class="schedule-section-level-item-signup-title">Записаться</span>
                <img class="schedule-section-level-item-signup-arrow-image" src="../assets/common/arrow.svg" alt="arrow"/>
            </div>
            <span v-else class="schedule-section-level-item-closed">набор закрыт</span>
        </div>
    </div>
</template>

<script>
    
    export default {
        props: {
            teacher: {},
            startTime: String,
            endTime: String,
            days: String,
            startDate: String,
            duration: String,
            price: Number,
            priceWithoutDiscount: Number,
            discountValue: Number,
            isAvailable: Boolean
        },
        computed: {
            timeString: function() {
                return this.startTime + ' - ' + this.endTime;
            },
            discountString: function() {
                return 'скидка ' + this.discountValue + '%';
            }
        },
        methods: {
            showModal(name) {
                this.$modal.show(name)
            },
            checkSmallPhoto(teacher) {
                return teacher && teacher.smallPhoto;
            },
            checkName(teacher) {
                return teacher && teacher.name;
            },
            checkPosition(teacher) {
                return teacher && teacher.position;
            }
        }
    }
</script>

<style scoped>

    .schedule-section-level-item-container {
        display: flex;
        align-items: center;
        padding: 2.2rem 0;
    }
    
    .schedule-section-level-item-teacher-container {
        display: flex;
        width: 24rem;
    }
    
    .schedule-section-level-item-teacher-photo {
        width: 4rem;
        height: 4rem;
        margin-left: 4rem;
    }
    
    .schedule-section-level-item-teacher-info-container {
        display: flex;
        flex-direction: column;
        margin-left: 2rem;
    }
    
    .schedule-section-level-item-teacher-name {
        font-family: GothamPro-Medium, sans-serif;
        font-size: 1.4rem;
        color: var(--tomato);
        margin: 0.2rem 0;
        text-align: left;
    }
    
    .schedule-section-level-item-teacher-name-empty {
        font-family: GothamPro, sans-serif;
        font-size: 1.4rem;
        margin: 0.2rem 0;
        text-align: left;
    }
    
    .schedule-section-level-item-teacher-post {
        font-family: GothamPro, sans-serif;
        font-size: 1.2rem;
        text-align: left;
        margin: 0.2rem 0;
    }
    
    .schedule-section-level-item-teacher-post-empty {
        font-family: GothamPro, sans-serif;
        font-size: 1.2rem;
        text-align: left;
        color: #ada391;
        margin: 0.2rem 0;
    }

    .schedule-section-level-item-time-info-container {
        display: flex;
        flex-direction: column;
        width: 20rem;
    }
    
    .schedule-section-level-item-time {
        font-family: GothamPro, sans-serif;
        font-size: 1.4rem;
        text-align: left;
        margin: 0.2rem 0;
    }
    
    .schedule-section-level-item-days {
        font-family: GothamPro, sans-serif;
        font-size: 1.2rem;
        text-align: left;
        margin: 0.2rem 0;
    }
    
    .schedule-section-level-item-signup-tablet {
        display: none;
        margin-top: 1rem;
        cursor: pointer;
    }
    
    .schedule-section-level-item-signup-mobile {
        display: none;
        margin-top: 1rem;
        cursor: pointer;
    }
    
    .schedule-section-level-item-start-date {
        font-family: GothamPro, sans-serif;
        font-size: 1.4rem;
        text-align: left;
        width: 14rem;
        box-sizing: border-box;
        margin-top: 0.2rem;
        align-self: flex-start;
    }
    
    .schedule-section-level-item-duration {
        font-family: GothamPro, sans-serif;
        font-size: 1.2rem;
        text-align: left;
        width: 20rem;
        align-self: flex-start;
        margin-top: 0.2rem;
        padding-right: 6rem;
        box-sizing: border-box;
    }
    
    .schedule-section-level-item-price-container {
        display: flex;
        width: 26rem;
    }
    
    .schedule-section-level-item-price-info-container {
        display: flex;
        flex-direction: column;
        margin-left: 4rem;
    }
    
    .schedule-section-level-item-price-without-discount {
        font-family: GothamPro, sans-serif;
        font-size: 1.4rem;
        text-decoration: line-through;
        margin: 0.2rem 0;
        position: relative;
    }
    
    .schedule-section-level-item-discount {
        font-family: GothamPro, sans-serif;
        font-size: 1.2rem;
        width: 8.5rem;
        height: 2rem;
        background-color: var(--main-color);
        border-radius: 0.2rem;
        text-align: center;
        display: flex;
        flex-direction: column;
        justify-content: center;
        position: absolute;
        left: -10rem;
        bottom: -0.2rem;
    }
    
    .schedule-section-level-item-price {
        font-family: GothamPro-Medium, sans-serif;
        font-size: 1.4rem;
        text-align: left;
        color: var(--tomato);
        margin: 0.2rem 0;
    }
    
    .schedule-section-level-item-signup-container {
        display: flex;
        align-items: center;
        margin-left: auto;
        text-decoration: none;
        color: black;
        cursor: pointer;
    }
    
    .schedule-section-level-item-signup-title {
        font-family: GothamPro-Bold, sans-serif;
        font-size: 1.2rem;
        text-transform: uppercase;
    }
    
    .schedule-section-level-item-signup-arrow-image {
        margin-left: 1rem;
    }
    
    .schedule-section-level-item-closed {
        font-family: GothamPro, sans-serif;
        font-size: 1.4rem;
        align-self: flex-start;
        margin-left: auto;
    }

    @media screen and (max-width: 1280px) {
        
        .schedule-section-level-item-container {
            padding: 2rem 0;
            flex-direction: row-reverse;
            justify-content: flex-end;
        }
        
        .schedule-section-level-item-start-date {
            display: none;
        }
        
        .schedule-section-level-item-duration {
            display: none;
        }
        
        .schedule-section-level-item-price-container {
            display: none;
        }
        
        .schedule-section-level-item-time-info-container {
            margin-left: 0;
            width: 50%;
        }
        
        .schedule-section-level-item-teacher-container {
            width: 50%;
        }
        
        .schedule-section-level-item-teacher-photo {
            margin-left: 2rem;
        }
        
        .schedule-section-level-item-signup-tablet {
            display: block;
        }
        
    }

    @media screen and (max-width: 760px) {
        
        .schedule-section-level-item-teacher-info-container {
            display: none;
        }
        
        .schedule-section-level-item-teacher-container {
            align-self: flex-start;
        }
        
        .schedule-section-level-item-teacher-photo {
            margin-left: auto;
        }

        .schedule-section-level-item-signup-tablet {
            display: none;
        }
        
        .schedule-section-level-item-signup-mobile {
            display: block;
        }
        
    }

</style>