<template>
    <div v-if="type === 'normal'" class="teacher-card-container">
        <img v-if="image" class="teacher-card-image" :src="image" :alt="name">
        <img v-else class="teacher-card-image" src="../assets/teachers/teacher-default.svg" :alt="name">
        <div class="teacher-card-title">{{name}}</div>
        <div class="teacher-card-city">{{city}}</div>
        <div class="teacher-card-languages-container">
            <div class="teacher-card-language"
                  v-for="(language, index) in languages" 
                  :class="language.color"
                  :key="index">
                {{language.name}}
            </div>
        </div>
        <div v-if="shortDescription" class="teacher-card-description">{{shortDescription | trim(160)}}</div>
    </div>
    <div v-else-if="type === 'small'" class="teacher-card-container-small">
        <img v-if="image" class="teacher-card-image-small" :src="image" :alt="name">
        <img v-else class="teacher-card-image-small" src="../assets/teachers/teacher-default.svg" :alt="name">
        <div class="teacher-card-title-small">{{name}}</div>
        <div class="teacher-card-city-small">{{city}}</div>
    </div>
</template>

<script>

    export default {
        props: {
            image: String,
            imageLarge: String,
            name: String,
            city: String,
            languages: Array,
            shortDescription: String,
            description: String,
            type: String
        },
        data() {
            return {
                isModalVisible: false,
            }
        },
        filters: {
            trim(value, count) {
                return value.substring(0, count);
            }
        }
    }
</script>

<style scoped>

    .teacher-card-container {
        display: flex;
        flex-direction: column;
        width: 28rem;
        height: 50rem;
        align-items: center;
    }
    
    .teacher-card-container-small {
        display: flex;
        flex-direction: column;
        width: 10rem;
        height: 18rem;
        align-items: center;
    }
    
    .teacher-card-image {
        width: 18rem;
        min-width: 18rem;
        height: 22.5rem;
        min-height: 22.5rem;
    }
    
    .teacher-card-image-small {
        width: 10rem;
        min-width: 10rem;
        height: 12.5rem;
        min-height: 12.5rem;
    }
    
    .teacher-card-title {
        font-family: FedraSerifAPro-Medium, sans-serif;
        font-size: 2.4rem;
        margin-top: 3rem;
    }
    
    .teacher-card-title-small {
        font-family: GothamPro-Medium, sans-serif;
        font-size: 1.8rem;
        margin-top: 1rem;
    }
    
    .teacher-card-city {
        font-family: GothamPro-Medium, sans-serif;
        font-size: 1.4rem;
        margin-top: 1rem;
    }
    
    .teacher-card-city-small {
        font-family: GothamPro, sans-serif;
        font-size: 1.4rem;
        margin-top: 0.5rem;
    }
    
    .teacher-card-languages-container {
        display: flex;
        align-items: center;
        justify-content: center;
        margin-top: 2.5rem;
    }
    
    .teacher-card-language {
        font-family: GothamPro-Bold, sans-serif;
        font-size: 1rem;
        text-transform: uppercase;
        padding: 0.8rem 1.2rem;
        margin: 0 0.6rem;
    }
    
    .yellow {
        color: #ffbc00;
        border: solid 0.1rem #ffbc00;
        border-radius: 0.4rem;
    }
    
    .red {
        color: var(--tomato);
        border: solid 0.1rem var(--tomato);
        border-radius: 0.4rem;
    }
    
    .teacher-card-description {
        font-family: GothamPro, sans-serif;
        font-size: 1.4rem;
        line-height: 1.71;
        margin-top: 2.5rem;
    }

    @media screen and (max-width: 760px) {
        
        .teacher-card-container {
            height: 36rem;
        }
        
        .teacher-card-image {
            width: 10.8rem;
            min-width: 10.8rem;
            height: 13.5rem;
            min-height: 13.5rem;
        }
        
        .teacher-card-title {
            font-size: 1.6rem;
            margin-top: 1.5rem;
        }
        
        .teacher-card-city {
            font-size: 1.2rem;
        }
        
        .teacher-card-description {
            font-size: 1.2rem;
            line-height: 1.5;
        }
        
    }
    
</style>