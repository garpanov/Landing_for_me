<script setup>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { onMounted } from 'vue';

gsap.registerPlugin(ScrollTrigger)



function section_1() {
  const tm_1 = gsap.timeline()

  tm_1.from('.text-1-h1', { x: -100, stagger: 0.2, opacity: 0 })
    .from('.text-1-p', { y: 100, opacity: 0, stagger: 0.2, duration: 1 }, 0.5)
    .from('.logo', { y: -50, opacity: 0 }, 0.8)
    .from('.element_1_left', { x: -50, opacity: 0, stagger: 0.1 }, 1)
    .from('.element_1_center', { y: 50, opacity: 0, stagger: 0.1 }, 1.4)
    .from('.element_1_right', { x: 50, opacity: 0, stagger: 0.1 }, 1.8)
    .from('.cloud', { y: -100, opacity: 0, duration: 1 }, 2)


  gsap.fromTo('.text-1-h1', { y: 0 }, {
    scrollTrigger: {
      trigger: '.block-text-1',
      start: `-150 top`,
      scrub: true
    },
    y: -100,
    opacity: 0.3
  })

  gsap.fromTo('.text-1-p', { y: 0 }, {
    scrollTrigger: {
      trigger: '.block-text-1',
      start: `-150 top`,
      scrub: true
    },
    y: 20,
    opacity: 0.1
  })

  gsap.to('.elements_1', {
    scrollTrigger: {
      trigger: '.block-text-1',
      start: `-100 top`,
      scrub: true
    },
    scale: 1.25,
    x: -200
  })
}

function section_2(for_end, for_console) {

  gsap.from('.text-2-h1', {
    scrollTrigger: {
      trigger: '.block_2',
      start: 'top bottom',
      end: `${for_end} center`,
      scrub: true
    },
    x: -100,
    opacity: 0,
    stagger: 0.2
  })

  gsap.from('.vector_1', {
    scrollTrigger: {
      trigger: '.block_2',
      start: 'center bottom'
    },
    scale: 0,
    opacity: 0,
    x: 100
  })

  const tm_2 = gsap.timeline({
    scrollTrigger: {
      trigger: '.block_2',
      start: `${for_console} bottom`,
      toggleActions: 'restart none none none' // Запуск при появі
    }
  });

  tm_2.from('.consol', { x: 50, opacity: 0, scale: 0.5, duration: 0.5},
            ).from('.code', {x:-50, opacity: 0, scale:0.9, stagger:0.1})
            .from('.text-2-p', {x: -100, opacity:0, stagger:0.5, ease: "bounce.out"}, 1.3)
            .from('.vector_2', {y: 100, x: -50, opacity: 0, scale:0.8, duration: 0.5}, 2.5)
            .from('.brackets_1', {y: -100, opacity: 0, scale: 0.7, duration: 0.5}, 2.8)
}

function section_3() {
  const tm_3_logo = gsap.timeline({scrollTrigger: {trigger: '.bottom_3', start: 'bottom bottom'}})
  tm_3_logo.from('.top_3', { x: -100, opacity: 0 }).from('.bottom_3', { x: 100, opacity: 0}, 0.2)

  gsap.from('.text-3-h1', {
    scrollTrigger: {
      trigger: '.block_3',
      start: 'top bottom',
      end: `bottom bottom`,
      scrub: true
    },
    x: -100,
    opacity: 0,
    stagger: 0.2
  })

  gsap.to('.laptop', {
    scrollTrigger: {trigger: '.laptop', start: 'top center', scrub: true},
      x: -50
  })

  gsap.from('.text-3-p', {scrollTrigger: { trigger: '.text-3-p', start: 'bottom bottom'},
                            y: 100, opacity: 0, scale: 0.5, x: -50})
  
  gsap.to(".text-3-h2", {
    x: "-110%",  // Рухається вліво
    duration: 5, // Час анімації
    ease: "linear", // Рівномірний рух
    repeat: -1, // Безкінечний повтор
});
}

function section_4(change_size_h1, change_size_black) {
  gsap.to('.text-4-h1', { scrollTrigger: { trigger: '.block_4', start: 'top bottom', scrub: true },
                          x: change_size_h1, y: -50 })

  gsap.to('.space-gray', { scrollTrigger: { trigger: '.space-gray', start: 'top bottom', scrub: true },
                            y: -100, scale:0.95})
  gsap.to('.Black', { scrollTrigger: { trigger: '.Black', start: 'top bottom', scrub:true },
                      x: change_size_black, y: -40 })

  gsap.from('.text-4-p', { scrollTrigger: { trigger: '.block_4_1', start: 'bottom bottom' },
                            y: 100, opacity: 0, stagger: 0.2})
  
  gsap.from('.elements_4', { scrollTrigger: { trigger: '.block_4_1', start: 'top bottom', scrub: true },
                              y: 100, stagger:0.2})
}

function section_footer() {
  const tm_5 = gsap.timeline({ scrollTrigger: { trigger: '.text-5-h1', start: 'bottom bottom' }})
  tm_5.from('.text-5-h1', { x: -300, opacity: 0, direction: 0.5 })
  .from('.union', { y: -50, opacity: 0 }, 0.3)

  gsap.from('.socials', { scrollTrigger: { trigger: '.socials', start: 'top bottom', scrub: true },
                          y: -150})

  gsap.from('.copyright', { scrollTrigger: { trigger: '.copyright', start: 'bottom bottom', toggleActions: 'restart none none none'},
                            y: -100, opacity: 0 })
}

onMounted(() => {
  const size_window = window.innerWidth
  console.log(size_window)
  section_1()

  if (size_window >= 1536) {
    section_2('bottom', 'bottom')
  }
  else if (size_window >= 1024) {
    section_2('bottom', 'center')
  }
  else if (size_window >= 300) {
    section_2('center', 'center')
  }

  section_3()

  if (size_window >= 700) {
    section_4(100, 60)
  }
  else if (size_window >= 400) {
    section_4(40, 10)
  }
  
  section_footer()
})
</script>

<template>
  <div class="block_1 bg-black h-full pb-40 w-full">
    <header class="py-5 px-10 flex gap-5">
      <div class="logo w-6 h-6 md:w-8 md:h-8 lg:w-10 lg:h-10 rounded-full bg-gradient-to-r from-[#0BFF2F] to-[#F223F5]">
      </div>
      <h1 class="logo header-text text-white text-xl md:text-2xl lg:text-3xl ">D.E.V Satoshi</h1>
    </header>
    <img class="cloud absolute ml-20 xl:ml-120 lg:ml-40 xl:ml-160 2xl:ml-210 mt-50 md:mt-55 lg:mt-65 xl:mt-10"
      src="../public/1/Union.png">

    <div class="hidden xl:flex flex-col xl:flex-row h-3/4">
      <div class="block-text-1 w-full text-center xl:text-left xl:w-3/6 h-full mt-20 xl:mt-50 ml-0 xl:ml-20 text-white">
        <h1 class="text-1-h1 text-4xl xl:text-7xl tracking-wider">New design with</h1>
        <h1 class="text-1-h1 text-4xl xl:text-7xl tracking-wider">a new applications</h1>
        <p class="text-1-p text-2xl xl:text-5xl mt-20 xl:mt-10">Cutting-edge apps, bold design, and</p>
        <p class="text-1-p text-2xl xl:text-5xl">rock-solid code. No nonsense — just</p>
        <p class="text-1-p text-2xl xl:text-5xl">results</p>
      </div>
      <div class="elements_1 xl:w-3/6 xl:h-4/6 mt-30 xl:mr-10 flex z-30">

        <div class="flex flex-col gap-3">
          <img src="../public/1/figures/Ellipse 5.png" class="element_1_left" data-spead="0.35">
          <img src="../public/1/figures/Rectangle 2.png" class="element_1_left" data-speed="0.15">
          <img src="../public/1/figures/Rectangle 5.png" class="element_1_left" data-speed="0.23">
        </div>
        <div class="flex flex-col gap-3">
          <img src="../public/1/figures/Ellipse 8.png" class="element_1_left" data-speed="0.14">
          <img src="../public/1/figures/Rectangle 3.png" class="element_1_left" data-speed="0.23">
        </div>
        <div class="flex flex-col gap-3">
          <img src="../public/1/figures/Ellipse 1.png" class="element_1_center" data-speed="0.11">
          <img src="../public/1/figures/Rectangle 11.png" width="155" class="element_1_center" data-speed="0.17">
          <img src="../public/1/figures/Ellipse 3.png" class="element_1_center" data-speed="0.33">
        </div>
        <div class="flex flex-col gap-3">
          <img src="../public/1/figures/Rectangle 8.png" class="element_1_right" data-speed="0.42">
          <img src="../public/1/figures/Rectangle 1.png" class="element_1_right" data-speed="0.19">
        </div>
        <div class="flex flex-col gap-3">
          <img src="../public/1/figures/Ellipse 8.png" class="element_1_right" data-speed="0.37">
          <img src="../public/1/figures/Rectangle 4.png" class="element_1_right" data-speed="0.17">
          <img src="../public/1/figures/Ellipse 7.png" class="element_1_right" data-speed="0.25">
        </div>
      </div>
    </div>

    <div class="flex xl:hidden flex-col xl:flex-row h-3/4">
      <div
        class="w-full block-text-1 flex flex-col items-center content-center text-center xl:text-left xl:w-3/6 h-full mt-20 xl:mt-50 ml-0 xl:ml-20 text-white">
        <h1 class="text-1-h1 text-4xl md:text-6xl lg:text-7xl tracking-wider">New design with</h1>
        <h1 class="text-1-h1 text-4xl md:text-6xl lg:text-7xl tracking-wider">a new applications</h1>
        <div class="w-11/12 xl:w-3/6 xl:h-4/6 mt-30 flex z-30">

          <div class="flex flex-col gap-3">
            <img src="../public/1/figures/Ellipse 5.png" class="element_1_left">
            <img src="../public/1/figures/Rectangle 2.png" class="element_1_left">
            <img src="../public/1/figures/Rectangle 5.png" class="element_1_left">
          </div>
          <div class="flex flex-col gap-3">
            <img src="../public/1/figures/Ellipse 8.png" class="element_1_left">
            <img src="../public/1/figures/Rectangle 3.png" class="element_1_left">
          </div>
          <div class="flex flex-col gap-3">
            <img src="../public/1/figures/Ellipse 1.png" class="element_1_center">
            <img src="../public/1/figures/Rectangle 11.png" width="155" class="element_1_center">
            <img src="../public/1/figures/Ellipse 3.png" class="element_1_center">
          </div>
          <div class="flex flex-col gap-3">
            <img src="../public/1/figures/Rectangle 8.png" class="element_1_right">
            <img src="../public/1/figures/Rectangle 1.png" class="element_1_right">
          </div>
          <div class="flex flex-col gap-3">
            <img src="../public/1/figures/Ellipse 8.png" class="element_1_right">
            <img src="../public/1/figures/Rectangle 4.png" class="element_1_right">
            <img src="../public/1/figures/Ellipse 7.png" class="element_1_right">
          </div>
        </div>
        <p class="text-1-p text-2xl md:text-4xl lg:text-5xl mt-20 xl:mt-10">Cutting-edge apps, bold design, and</p>
        <p class="text-1-p text-2xl md:text-4xl lg:text-5xl">rock-solid code. No nonsense — just</p>
        <p class="text-1-p text-2xl md:text-4xl lg:text-5xl">results</p>
      </div>
    </div>
  </div>
  <div class="block_2 flex flex-col lg:flex-row items-center lg:items-start bg-white h-full pb-30 lg:pb-50 w-full">
    <div class="hidden lg:flex">
      <div class="flex w-3/6 mt-30 ml-20">
        <div>
          <div>
            <h1 class="text-2-h1 lg:text-7xl xl:text-8xl">Creating Telegram</h1>
            <h1 class="text-2-h1 lg:text-7xl xl:text-8xl">and Discord bots</h1>
          </div>
          <div class="mt-50">
            <p class="text-2-p tracking-wider text-7xl">No holds</p>
            <img src="../public/2/vector2.png" class="vector_2 lg:ml-110 xl:ml-130">
            <p class="text-2-p tracking-wider text-7xl">barred</p>
          </div>
        </div>
        <div></div>
      </div>
      <img src="../public/2/Brackets 1.png"
        class="brackets_1 absolute z-1 lg:mt-105 xl:mt-145 2xl:mt-155 lg:ml-110 xl:ml-150 2xl:ml-200 lg:scale-50 xl:scale-100">
      <div class="flex flex-col w-3/6">
        <img src="../public/2/Vector.png" class="vector_1 absolute w-40 xl:w-50 right-10 xl:right-15 xl:mt-10">
        <div class="flex">
          <img src="../public/2/Component 1.png" class="consol h-80 lg:h-90 xl:h-120 2xl:h-150 lg:mt-80 2xl:mt-60 z-2">
          <div class="flex-col absolute lg:mt-95 xl:mt-100 2xl:mt-80 2xl:mt-85 lg:ml-5 xl:ml-10 z-2">
            <div class="flex lg:gap-5 xl:gap-10">
              <p class="code text-2-import lg:text-4xl xl:text-5xl">import</p>
              <p class="code text-2-code lg:text-4xl xl:text-5xl">aiogram</p>
            </div>
            <div class="flex lg:gap-5 xl:gap-10 mt-3">
              <p class="code text-2-import lg:text-4xl xl:text-5xl">import</p>
              <p class="code text-2-code lg:text-4xl xl:text-5xl">asyncio</p>
            </div>
            <div class="lg:mt-10 xl:mt-20">
              <p class="code text-2-code lg:text-4xl xl:text-5xl">bot = Bot(TOKEN)</p>
              <p class="code text-2-code lg:text-4xl xl:text-5xl lg:mt-2 xl:mt-5">dp = Dispatcher()</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="flex lg:hidden">
      <img src="../public/2/Vector.png" class="vector_1 absolute w-30 right-10 mt-10">
      <div class="flex mt-50">
        <div>
          <div class="flex flex-col items-center">
            <h1 class="text-2-h1 text-5xl">Creating Telegram</h1>
            <h1 class="text-2-h1 text-5xl">and Discord bots</h1>
          </div>
          <div class="flex flex-col">
            <div class="flex justify-center">
              <img src="../public/2/Component 1.png" class="consol h-1/4 w-85 mt-20 z-2">
              <div class="code flex-col absolute mt-30 mr-10 z-2">
                <div class="flex gap-5">
                  <p class="code text-2-import text-2xl">import</p>
                  <p class="code text-2-code text-2xl">aiogram</p>
                </div>
                <div class="flex gap-5 mt-3">
                  <p class="code text-2-import text-2xl">import</p>
                  <p class="code text-2-code text-2xl">asyncio</p>
                </div>
                <div class="mt-5">
                  <p class="code text-2-code text-2xl">bot = Bot(TOKEN)</p>
                  <p class="code text-2-code text-2xl mt-1">dp = Dispatcher()</p>
                </div>
              </div>
            </div>
          </div>
          <div class="mt-30 ml-5">
            <p class="text-2-p tracking-wider text-5xl">No holds</p>
            <img src="../public/2/vector2.png" class="vector_2 w-15 ml-70 md:ml-80">
            <p class="text-2-p tracking-wider text-5xl">barred</p>
          </div>
        </div>
        <div></div>
      </div>
      <img src="../public/2/Brackets 1.png" class="brackets_1 absolute z-1 w-50 mt-136 md:mt-133">

    </div>
  </div>
  <div class="block_3 bg-black w-full">
    <div class="flex p-1 xl:p-10">
      <img src="../public/3/Top.png" class="top_3 ml-10 xl:ml-40 w-25 xl:w-40 mt-10 xl:mt-5">
      <img src="../public/3/Bottom.png" class="bottom_3 absolute w-25 xl:w-40 ml-10 xl:ml-40 mt-20 xl:mt-13 xl:mt-23 xl:mt-20">
    </div>
    <div class="flex ml-10 xl:ml-20 mt-40 xl:mt-20 pb-200 xl:pb-250">
      <div class="hidden md:block">
        <h1 class="text-3-h1 text-4xl md:text-6xl xl:text-8xl">Building websites </h1>
        <h1 class="text-3-h1 text-4xl md:text-6xl xl:text-8xl mt-10">that hit hard and </h1>
        <h1 class="text-3-h1 text-4xl md:text-6xl xl:text-8xl mt-10">leave a mark </h1>
      </div>

      <div class="block md:hidden">
        <h1 class="text-3-h1 text-4xl xl:text-8xl">Building</h1>
        <h1 class="text-3-h1 text-4xl xl:text-8xl mt-3">websites that hit</h1>
        <h1 class="text-3-h1 text-4xl xl:text-8xl mt-3">hard and leave a </h1>
        <h1 class="text-3-h1 text-4xl xl:text-8xl mt-3">mark</h1>
      </div>
      <img src="../public/3/Laptop 1.png" class="laptop absolute mt-30 md:mt-40 lg:mt-5 xl:mt-60 2xl:mt-10 w-4/6 right-0 z-30">
      <!-- <h2 class="absolute whitespace-nowrap text-3-h2 z-10 text-8xl mt-200">Start your modern journey with cutting-edge technology.</h2> -->

      <div class="hidden md:block absolute xl:right-30 mt-150 xl:mt-270">
        <p class="text-3-p text-4xl md:mt-10 md:text-5xl">Stay ahead, stay sharp, be at</p>
        <p class="text-3-p text-4xl md:mt-10 md:text-5xl">the center of what’s next</p>
      </div>
      <div class="block md:hidden absolute xl:right-30 mt-120 xl:mt-270">
        <p class="text-3-p text-4xl">Stay ahead, stay</p>
        <p class="text-3-p text-4xl mt-3">sharp, be at</p>
        <p class="text-3-p text-4xl mt-3">the center of</p>
        <p class="text-3-p text-4xl mt-3">what’s next</p>
      </div>

    </div>
  </div>
  <div class="block_4 bg-black pb-200 lg:pb-220 xl:pb-200 w-full border">
    <div class="flex xl:ml-20 pt-5 xl:pt-20">
      <div class="hidden ml-5 xl:block">
        <h1 class="text-4-h1 text-4xl xl:text-8xl">Adaptability for any</h1>
        <h1 class="text-4-h1 text-4xl xl:text-8xl">device</h1>
      </div>
      <div class="block ml-5 xl:hidden">
        <h1 class="text-4-h1 text-6xl md:text-8xl">Adaptability <br> for any</h1>
        <h1 class="text-4-h1 text-6xl md:text-8xl">device</h1>
      </div>

      <img src="../public/4/Black.png"
        class="Black absolute w-40 md:w-50 ml-53 md:ml-85 lg:ml-150 md:scale-125 lg:scale-150 xl:scale-100 xl:w-120 xl:ml-10 2xl:ml-30 mt-20 md:mt-40 lg:mt-20 xl:mt-80">
      <div class="absolute ml-10 md:ml-50 lg:ml-110 xl:ml-150 2xl:ml-200 mt-100 xl:mt-20">
        <img src="../public/4/Space-Gray.png" class="space-gray w-90 md:w-110 lg:w-150 xl:w-230 md:mt-30 xl:mt-0 ">
        <div class="block_4_1 hidden xl:flex xl:gap-2 2xl:gap-10 mt-30 xl:mt-20">
          <div class="flex-col">
            <p class="text-4-p text-5xl xl:text-6xl">Unlocking</p>
            <p class="text-4-p mt-4 xl:mt-5 text-5xl xl:text-6xl">opportunities for</p>
            <p class="hidden xl:block text-4-p mt-5 text-6xl">users at all levels</p>
            <p class="block xl:hidden text-4-p mt-4 xl:mt-5 text-5xl xl:text-6xl">users at <br> all levels</p>
          </div>
          <div>
            <img src="../public/4/5.png" class="elements_4 absolute xl:scale-75 2xl:scale-100 z-5">
            <img src="../public/4/4.png" class="elements_4 absolute xl:scale-75 2xl:scale-100 mt-10 z-4">
            <img src="../public/4/3.png" class="elements_4 absolute xl:scale-75 2xl:scale-100 mt-20 z-3">
            <img src="../public/4/2.png" class="elements_4 absolute xl:scale-75 2xl:scale-100 mt-30 z-2">
            <img src="../public/4/1.png" class="elements_4 absolute xl:scale-75 2xl:scale-100 mt-40 z-1">
          </div>
        </div>

        <div class="block_4_1 flex xl:hidden gap-10 ml-0 mt-20 justify-center">
          <div class="flex-col">
            <p class="text-4-p text-5xl md:text-6xl">Unlocking</p>
            <p class="text-4-p mt-4 xl:mt-5 text-5xl md:text-6xl">opportunities for</p>
            <div class="flex">
              <div class="flex-col">
                <p class="hidden xl:block text-4-p mt-5 text-5xl md:text-6xl">users at all levels</p>
                <p class="block xl:hidden text-4-p mt-4 xl:mt-5 text-5xl md:text-6xl">users at <br> all levels</p>
              </div>
              <div class="flex-col ml-10 md:ml-15 mt-5">
                <img src="../public/4/5.png" class="elements_4 absolute w-30 z-5">
                <img src="../public/4/4.png" class="elements_4 absolute w-30 mt-6 z-4">
                <img src="../public/4/3.png" class="elements_4 absolute w-30 mt-12 z-3">
                <img src="../public/4/2.png" class="elements_4 absolute w-30 mt-18 z-2">
                <img src="../public/4/1.png" class="elements_4 absolute w-30 mt-24 z-1">
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
  <footer class="bg-black pt-60 xl:pt-60 w-full">
    <div class="flex justify-center items-center gap-10">
      <h1 class="text-5-h1 text-5xl xl:text-7xl">Contacts</h1>
      <img src="../public/5/Union.png" class="union w-25">
    </div>
    <div class="flex flex-col lg:flex-row lg:gap-15 xl:gap-20 justify-center items-center mt-30 xl:mt-40">
      <div onclick="window.open('https://discord.com/users/574597793558167552', '_blank')" class="hover:cursor-pointer socials flex gap-5 items-center  w-9/12 md:w-4/12 lg:w-1/4 justify-between lg:justify-center">
        <img src="../public/5/Vector (1).png" class="scale-60 xl:scale-100">
        <h2 class="text-5-h2 text-2xl xl:text-4xl">@Garpanov</h2>
      </div>
      <div onclick="window.open('https://github.com/garpanov', '_blank')" class="hover:cursor-pointer socials flex gap-5 items-center w-9/12 md:w-4/12 lg:w-1/4 justify-between lg:justify-center">
        <img src="../public/5/Vector.png" class="scale-60 xl:scale-100">
        <h2 class="text-5-h2 text-2xl xl:text-4xl">@Garpanov</h2>
      </div>
      <div onclick="window.open('https://t.me/ShadowCryps', '_blank')" class="hover:cursor-pointer socials flex gap-5 items-center w-9/12 md:w-4/12 lg:w-1/4 justify-between lg:justify-center">
        <img src="../public/5/Vector (2).png" class="scale-60 xl:scale-100">
        <h2 class="text-5-h2 text-2xl xl:text-4xl">@ShadowCryps</h2>
      </div>
    </div>
    <p class="copyright text-5-p text-lg text-center pt-10 xl:pt-50 pb-10">© 2025 D.E.V Satoshi</p>
  </footer>
</template>

<style lang="css">
.header-text {
  font-family: 'Roboto', sans-serif;
  font-weight: 900;
}

.text-1-h1 {
  font-family: "Roboto Slab", serif;
  font-weight: 500;
}

.text-1-p {
  font-family: 'Roboto Slab', serif;
  font-weight: 400;
}

.text-2-h1 {
  font-family: "Roboto Slab", serif;
  font-weight: 500;
}

.text-2-p {
  font-family: 'Rock Salt', serif;
  font-weight: 400;
}

.text-2-import {
  font-family: "IBM Plex Mono", monospace;
  font-weight: 500;
  color: #5D3DED;
}

.text-2-code {
  font-family: "IBM Plex Mono", monospace;
  font-weight: 500;
  color: white;
}

.text-3-h1 {
  font-family: "Roboto Slab", serif;
  font-weight: 800;
  color: white;
}

.text-3-h2 {
  font-family: "Roboto Slab", serif;
  font-weight: 900;
  color: white;
}

.text-3-p {
  font-family: "Roboto Slab", serif;
  font-weight: 300;
  color: white;
}

.text-4-h1 {
  font-family: "Roboto Slab", serif;
  font-weight: 800;
  color: white;
}

.text-4-p {
  font-family: "Rum Raisin", sans-serif;
  font-weight: 400;
  color: white;
}

.text-5-h1 {
  font-family: "Roboto Slab", serif;
  font-weight: 800;
  color: white;
}

.text-5-h2 {
  font-family: "Roboto Slab", serif;
  font-weight: 800;
  color: white;
}

.text-5-p {
  font-family: "Roboto Slab", serif;
  font-weight: 800;
  color: white;
}
</style>
