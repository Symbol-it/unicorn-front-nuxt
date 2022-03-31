<template>
    <div class="unicorn-card">
        <div class="unicorn-card__bloc-photo">
            <picture-found class="unicorn-card__bloc-photo__image" :unicorn="unicorn" />
            <!--<img v-if="pictureFound" class="unicorn-card__bloc-photo__image" :src="srcImage">
            <img v-else class="unicorn-card__bloc-photo__image" src="~assets/icons/not-found-image.jpg">-->
        </div>
        <div class="unicorn-card__name">
            Nom : <span>{{ unicorn.name }}</span>
        </div>
        <div class="unicorn-card__button">
            <unicorn-button :to="toTest">Voir plus</unicorn-button>
        </div>
    </div>
</template>
<script>
import UnicornButton from '@/components/UnicornButton'
import PictureFound from '@/components/PictureFound';
export default {
    name: 'UnicornCard',
    components: {
        UnicornButton,
        PictureFound
    },
    props: {
        unicorn: {
            type: Object,
            required: true
        }
    },
    computed: {
        srcImage () {
            return 'http://localhost:1337' + this.unicorn.photo.url || '';
        },
        toTest () {
            return `/${this.unicorn.id}`;
        },
        getUnicorn(){
          return this.unicorn;
        }
    }
}
</script>
<style scoped>
.unicorn-card {
  min-width: 200px;
  background-color: aliceblue;
  border-radius: 15px;
  border: 1px solid #7EA8EF;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.unicorn-card__bloc-photo {
  text-align: center;
}

/*.unicorn-card__bloc-photo__image img{
  margin-top: 15px;
  border-radius: 100%;
  width: 144px;
  height: 144px;
  object-fit: cover;
  object-position: center;
}*/

.unicorn-card__name {
  text-align: center;
  font-weight: bold;
}

.unicorn-card__name span {
  font-weight: normal;
}

.unicorn-card__button {
  margin: 20px 0;
  text-align: center;
}
</style>
