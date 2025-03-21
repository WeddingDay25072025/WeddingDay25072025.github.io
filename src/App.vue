<script setup>
import { onMounted, ref, watch } from 'vue';
import gsap, { SteppedEase } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { MotionPathPlugin } from 'gsap/all';

ScrollTrigger.config({ ignoreMobileResize: true });
gsap.registerPlugin(ScrollTrigger);
gsap.registerPlugin(MotionPathPlugin);
const video = ref(null)
const quests = ref(null)
onMounted(() => {
  quests.value.forEach((el, index) => {
    gsap.from(el, {
      scrollTrigger: {
        scroller: 'body',
        trigger: el,
        start: '-80px 100%',
        toggleActions:'restart none none none',
      },
      x: index % 2 ? -320 : 320,
      duration: 1.2,
    });
  })
  gsap.from(".card1", {
    scrollTrigger: {
      scroller: 'body',
      start: '-20px 120%',
      trigger: '.card1',
      toggleActions:'restart none none none',
    },
    duration: 0.8,
    opacity: 0.2,
    y: 80,
  });
  gsap.from(".card2", {
    scrollTrigger: {
      scroller: 'body',
      start: '-20px 120%',
      trigger: '.card2',
      toggleActions:'restart none none none',
    },
    duration: 0.8,
    opacity: 0.2,
    y: 80,
  });

  gsap.to(".heart", {
    duration: 6,
    motionPath: [{ rotate: 8 }, { rotate: -8 }, { rotate: 8 }],
    transformOrigin: '50px 60px',
    yoyo: true,
    ease: "linear",
    repeat: -1,
  });

  const loader = document.getElementById('loader');
  const video = document.getElementById('video');

  // Показываем лоудер при загрузке видео
  video.addEventListener('loadstart', () => {
      loader.style.display = 'block';
  });

  // Скрываем лоудер, когда видео загружено
  video.addEventListener('canplaythrough', () => {
      loader.style.display = 'none';
  });

  // Скрываем лоудер, если произошла ошибка
  video.addEventListener('error', () => {
      loader.style.display = 'none';
      alert('Ошибка загрузки видео.');
  });
})

const handleClickByVideo = () => {
  const myVideo = video.value
  if (myVideo.paused) {
    if (myVideo.requestFullscreen) {
        myVideo.requestFullscreen();
    }
    else if (myVideo.msRequestFullscreen) {
        myVideo.msRequestFullscreen();
    }
    else if (myVideo.mozRequestFullScreen) {
        myVideo.mozRequestFullScreen();
    }
    else if (myVideo.webkitRequestFullScreen) {
        myVideo.webkitRequestFullScreen();
    }
    else if (video.webkitEnterFullScreen) {
        myVideo.webkitEnterFullScreen();
    }
    myVideo.play();
}
else {
    myVideo.pause();
}
}

const handleClickOpenMap = () => {
  window.open('https://yandex.by/maps/org/agrousadba_malinovka/130558307103/?ll=27.462270%2C52.679237&z=16.26')
}

const quests_options = [
  { id: 1, title: 'Цветы', text: 'Если вы планировали взять с собой букет цветов, то бутылочка алкоголя с вашей подписью будет лучшей заменой, так как мы не успеем насладиться красотой цветов до отъезда в путешествие!', flower: true},
  { id: 1, title: 'Дресс-код', text: 'Мы будем очень признательны, если при выборе нарядов вы отдадите предпочтение нежным пастельным тонам и воздержитесь от ярких цветов.', flower: false},
]
</script>

<template>
  <div class="main">
    <div class="container-video">
      <div class="container-video__img">
        <div id="loader" class="loader"></div>
        <video preload autoplay id="video" ref="video">
          <source src="./assets/video.mp4" type="video/mp4">
          <!-- <source src="./assets/video.webm" type="video/webm"> -->
        </video>
      </div>
      <div class="container-video__play" @click="handleClickByVideo">
        <i class="fa-solid fa-play"></i>
      </div>
    </div>
    <div class="after-video">
      <div class="lexend fz42 header_title">Дорогие гости</div>
      <div class="stand fz14">Мы приглашаем Вас разделить с нами радостный день, в который мы станем семьёй!</div>
    </div>
    <div class="sheduale">
      <div class="heart"></div>
      <div class="sheduale-weekdays">
        <div class="stand f500">ПН</div>
        <div class="stand f500">ВТ</div>
        <div class="stand f500">СР</div>
        <div class="stand f500">ЧТ</div>
        <div class="stand f500">ПТ</div>
        <div class="stand f500">СБ</div>
        <div class="stand f500">ВС</div>
      </div>
      <div class="sheduale-days">
        <div class="stand f400">21</div>
        <div class="stand f400">22</div>
        <div class="stand f400">23</div>
        <div class="stand f400">24</div>
        <div class="stand f600 color-bg">
          25
        </div>
        <div class="stand f600 color-bg">26</div>
        <div class="stand f400">27</div>
      </div>
      <div></div>
    </div>
    <div class="sicks">
      <div class="sick_one">
        <div class="lexend fz32">15:00</div>
        <div class="lexend fz32">Сбор гостей</div>
        <div class="stand fz14">Время пролетит незметно за игристыми и общением с другими гостями</div>
      </div>
      <div class="sick_two">
        <div class="lexend fz32">16:00</div>
        <div class="lexend fz32">Церемония</div>
        <div class="stand fz14">Вы станете свидетелями создания новой семьи - нашей семьи!</div>
      </div>
      <div class="sick_three">
        <div class="lexend fz32">17:00</div>
        <div class="lexend fz32">Банкет</div>
        <div class="stand fz14">Будет много танцев, веселья, поздравлений и, конечно, любви</div>
      </div>
    </div>
    <div class="cards">
      <div class="card card1">
        <div class="card-circle"></div>
        <div class="card-img">
          <img src="./assets/location.webp" alt="">
        </div>
      </div>
      <div class="card-after">
        <div class="card-after-title lexend fz36">Локация</div>
        <div class="card-after-subtitle stand fz16 f400">
          <span>
            Солигорский район <hr>
          </span>
          <span>
          Агроусадьба Малиновка <hr>
        </span></div>
        <div class="card-after-button stand fz12 f400" @click="handleClickOpenMap">Открыть карту</div>
      </div>
    </div>
    <div class="history">
      <div class="card card2">
        <div class="card-img">
          <img src="./assets/photo1.webp" alt="">
        </div>
        <div class="card-circle"></div>
      </div>
      <div class=" history-text stand fz14 ">Мы жили в одном городе, проходили мимо друг друга на улицах сотни раз, но впервые встретились на вечеринке у общих знакомых. Когда наши взгляды встретились, в воздухе словно заискрилось. В этот миг мы поняли, что между нами возникло что-то особенное — невидимая связь, которая обещала новые эмоции и приключения.</div>
    </div>
    <div class="question">
      <div class="lexend fz36">Несколько просьб</div>
      <div class="question-list">
        <div class="question-list-item" v-for="{ title, text, flower, id } in quests_options" :key="id" ref="quests">
          <div class="flower_3" v-if="flower"/>
          <div class="list-item-title lexend fz28">{{ title }}</div>
          <div class="list-item-text stand fz14 f400">{{ text }}</div>
        </div>
      </div>
    </div>
    <div class="lexend fz36 end-text">
      <span class="lexend fz28">С &nbsp; любовью,</span> <br> Сабина&nbsp;&nbsp; & &nbsp;&nbsp;Кирилл
    </div>
    <div class="lineTop" />
    <div class="flower4" />
    <div class="flower flower_2" />
    <div class="text-bg" />
    <div class="line"></div>
  </div>
</template>

<style scoped>

.main {
  position: relative;
  background-color: var(--color-bg-main);
  max-width: 320px;
  margin: 0 auto;
  width: 100%;
  min-height: 100dvh;
  height: 100%;
  color: var(--color-text-black);
  overflow: auto;
  overflow-x: hidden;
  display: flex;
  gap: 42px;
  flex-direction: column;
  box-shadow: 0 0 5px 5px rgba(253, 252, 248, 1);
}

@media screen and (max-width: 425px)  {
  .main {
    width: 100%;
    max-width: unset
  }
}

.container-video {
  margin-top: 120px;
  position: relative;
  z-index: 1;
}

.container-video__img {
  border-radius: 8px;
  height: 350px;
  width: 240px;
  margin: auto;
  overflow: hidden;
}
.container-video__img video,
.container-video__img img{
  width: 100%;
  height: 100%;
  object-fit: cover;
  cursor: pointer;
}

.container-video__play {
  position: absolute;
  z-index: 1;
  width: 50px;
  height: 50px;
  background-color: var(--color-bg);
  border-radius: 50%;
  left: 50%;
  transform: translateX(-50%);
  bottom: -25px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container-video__play i {
  font-size: 20px;
  padding-left: 2px;
  color: white;
}

.after-video {
  display: flex;
  flex-direction: column;
  gap: 18px;
  justify-content: center;
  align-items: center;
  text-align: center;
  width: calc(100% - 40px);
  max-width: 250px;
  margin: auto;
}

.sheduale {
  display: flex;
  flex-direction: column;
  gap: 18px;
  width: 280px;
  margin: auto;
  padding-bottom: 75px;
  background-color: var(--color-bg-main);
  box-shadow: 0 -5px 10px 10px #FDFCF8;
  position: relative;
  z-index: 1;
}

.sheduale-weekdays {
  display: grid;
  grid-template-columns: repeat(7 , 1fr);
  text-align: center;
  gap: 12px;
}

.sheduale-days {
  display: grid;
  grid-template-columns: repeat(7 , 1fr);
  text-align: center;
  gap: 12px;
}

.color-bg {
  color: var(--color-bg);
}

.heart {
  position: absolute;
  width: 158px;
    height: 162px;
    right: -13px;
    top: -8px;
  background-image: url('./assets/heart2.webp');
  background-repeat: no-repeat;
  background-size: contain;
  z-index: 1;
}

.heart::after {
  content: '';
  background-image: url('./assets/jule.webp');
  background-position: center;
  background-repeat: no-repeat;
  background-size: 200px;
  width: 100px;
  height: 100px;
  rotate: -20deg;
  position: absolute;
  right: 50px;
  bottom: -45px;
}

.sicks {
  display: flex;
  flex-direction: column;
  gap: 80px;
  width: calc(100% - 40px);
  margin: auto;
}

.sick_one,
.sick_two,
.sick_three {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.sick_one,
.sick_three {
  padding-right: 30%;
}

.sick_two {
  padding-left: 30%;
}

.sick_three {
  background-color: var(--color-bg-main);
  z-index: 1;
  padding: 10px;
  box-shadow: 0 0 10px 10px #FDFCF8;
}

.cards {
  display: flex;
  flex-direction: column;
  gap: 40px;
  width: calc(100% - 80px);
  margin: auto;
  z-index: 1;
}

.card {
  border: 8px solid var(--color-bg);
  border-radius: 6px;
  z-index: 1;
  position: relative;
  overflow: hidden;
  background-color: var(--color-bg);
  box-shadow: 0 2px 2px 2px rgba(0, 0, 0, 0.2);
}

.card-circle {
  position: absolute;
  width: 40px;
  height: 40px;
  background-color: var(--color-bg);
  border-radius: 50%;
  margin: auto;
  left: 50%;
  transform: translateX(-50%);
  top: -20px;
}

.card-after {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
  gap: 30px;
  border-radius: 6px;
  box-shadow: 0 2px 2px 2px rgba(0, 0, 0, 0.2);
}

.card-after-subtitle {
  margin-top: -5px;
  text-align: center;
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.card-after-subtitle hr {
  color: rgba(0, 0, 0, 0.2);
}

.card-img {
  border-radius: 4px;
  overflow: hidden;
  height: auto;
}

.card-img img {
  width: 100%;
  display: flex;
}

.card-after-button {
  background-color: var(--color-bg);
  color: white;
  padding: 15px 35px;
  border-radius: 12px;
  cursor: pointer;
}

.history {
  display: flex;
  position: relative;
  flex-direction: column;
  width: calc(100% - 80px);
  margin: auto;
  margin-top: 150px;
  gap: 20px;
}

.history-text {
  text-align: center;
}

.question {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-top: 50px;
  justify-content: center;
  align-items: center;
}

.question-list {
  display: flex;
  flex-direction: column;
  gap: 40px;
  width: calc(100% - 80px);
}

.question-list-item {
  position: relative;
  background-color: var(--color-bg);
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 15px;
  border-radius: 12px;
  overflow: hidden;
  padding-top: 50px;
}

.question-list-item::after {
  content: '';
  position: absolute;
  background-color: var(--color-bg-main);
  width: 60px;
  height: 60px;
  border-radius: 50%;
  left: 50%;
  transform: translateX(-50%);
  top: -30px;
}

.list-item-title {
  color: white;
}

.list-item-text {
  color: white;
  padding-right: 30px;
}

.flower {
  position: absolute;
  top: -80px;
  right: -80px;
  background-image: url('./assets/flower.webp');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: contain;
  width: 150px;
  rotate: 125deg;
  height: 150px;
}

.flower4 {
  position: absolute;
    top: -210px;
    right: -194px;
    background-image: url(/src/assets/flower4.webp);
    background-position: center center;
    background-repeat: no-repeat;
    background-size: 400px;
    width: 400px;
    rotate: 0DEG;
    height: 400px;
}


.flower_3 {
  position: absolute;
  top: -140px;
  right: -200px;
  background-image: url('./assets/flower3.webp');
  background-position: center center;
  background-repeat: no-repeat;
  rotate: -20deg;
  background-size: contain;
  aspect-ratio: 1;
  height: 400px;
}

.flower_2 {
  top: 820px;
  width: 200px;
  right: -100px;
  rotate: -50deg;
}

.line {
  position: absolute;
    top: 510px;
    rotate: 40deg;
    left: -415px;
    background-image: url(/src/assets/line.webp);
    background-position: center center;
    background-repeat: no-repeat;
    background-size: contain;
    aspect-ratio: 1;
    height: 1000px;
}

.lineTop {
  position: absolute;
    top: -310px;
    left: -255px;
    rotate: -234deg;
    background-image: url(/src/assets/lineTop.webp);
    background-position: center center;
    background-repeat: no-repeat;
    background-size: contain;
    aspect-ratio: 1;
    height: 925px;
}

.text-bg {
  position: absolute;
  top: 1820px;
  left: -188px;
  background-image: url('/src/assets/text2.webp');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: contain;
  aspect-ratio: 1;
  height: 758px;
}

.end-text {
  text-align: center;
  width: calc(100% - 40px);
  margin: auto;
  white-space: preline;
  padding-bottom: 30px;
}

@media screen and (max-width: 425px) {
  .end-text {
    width: calc(100% - 80px);
  }
}

.loader {
    margin: auto;
    position: absolute;
    left: 50%;
    top: 50%;
    transform-origin: center;
    width: 24px;
    height: 24px;
    border: 5px solid #801122;
    border-bottom-color: transparent;
    border-radius: 50%;
    animation: rotation 1s linear infinite;
    display: none;
    }

    @keyframes rotation {
    0% {
        transform: translate(-50%, -50%) rotate(0deg);
    }
    100% {
        transform: translate(-50%, -50%) rotate(360deg);
    }
    } 
</style>
