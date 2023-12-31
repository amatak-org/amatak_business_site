<script setup lang="ts">
import gsap from "gsap";
import Partner from "./Partner.vue";
import ServiceItem from "./ServiceItem.vue";

import Truck from "@/assets/svg/truck.svg";
import Freight from "@/assets/svg/freight.svg";
import Bicycle from "@/assets/svg/bicycle.svg";
import Warehouse from "@/assets/svg/warehouse.svg";
import Papers from "@/assets/svg/papers.svg";
import Chatbox from "@/assets/svg/chatbox.svg";

import Jumia from "@/assets/svg/jumia.svg";
import Amazon from "@/assets/svg/amazon.svg";
import Konga from "@/assets/svg/konga.svg";
import Etsy from "@/assets/svg/etsy.svg";
import Ebay from "@/assets/svg/ebay.svg";
import Macys from "@/assets/svg/macys.svg";

import { onMounted, ref } from "vue";
import { tweens } from "@/animations";

const section2Ref = ref<Nullable<HTMLElement>>(null);
let observerOptions = <IntersectionObserverInit>{
   threshold: 0.3,
};
const section2Observer = new IntersectionObserver(([{ isIntersecting }]) => {
   const tweenvar = isIntersecting ? 1 : 0;
   gsap.to(".Grid-Container > *", tweens.gridItemStaggerDrop[tweenvar]);
}, observerOptions);

onMounted(() => {
   let timeline = gsap.timeline();
   const section2 = section2Ref.value as HTMLElement;
   timeline.from(
      ".App-Services .Section-1 .Heading",
      tweens.fadeInFromBottom[0]
   );
   timeline.fromTo(
      ".App-Services .Section-1 .Line",
      tweens.lineExpand[0],
      tweens.lineExpand[1]
   );
   section2Observer.observe(section2);
});
</script>

<template>
   <main class="App-Services">
      <section class="Section Section-1">
         <h1 class="Heading">Our Services</h1>
         <hr class="Line" />
         <p class="Paragraph">
            Domain | Hosting | Website | SEO | Social Media.
         </p>
      </section>
      <section ref="section2Ref" class="Section Section-2">
         <br>
         <br>
         <div class="Grid-Container">

            <ServiceItem :src="Truck" alt="truck icon.">
               <template #heading> Procurement </template>
               Candace Logistics offers procurement and buyer representation to
               our customers, we buy, pick up, crate and package on your behalf,
               and ship either by air or sea to your final destination.
            </ServiceItem>
            <ServiceItem :src="Freight" alt="freight ship icon.">
               <template #heading> Freight Services </template>
               Cadence ships worldwide, containers and RoRos “Roll on Roll off”,
               whether you are shipping your car, household goods, motorhomes,
               tractors, heavy construction / earth moving equipment and general
               shipping, we can handle it all.
            </ServiceItem>
            <ServiceItem :src="Bicycle" alt="icon of person riding a bicycle.">
               <template #heading>Dispatch Delivery</template>
               Cadence provides the largest last-mile courier delivery solution
               in Nigeria. Send your parcels and packages with Cadence Go.
            </ServiceItem>
            <ServiceItem :src="Warehouse" alt="warehouse icon.">
               <template #heading> Warehousing </template>
               As an experienced logistics provider, we can help with any
               storage needs, for all long as is necessary.
            </ServiceItem>
            <ServiceItem :src="Papers" alt="icon of stacked papers.">
               <template #heading>Customs Clearance</template>
               Cadence will handle all processes involved in the transportation
               of your goods, including clearance.
            </ServiceItem>
            <ServiceItem :src="Chatbox" alt="message chat icon.">
               <template #heading> 24/7 Support </template>
               Lorem ipsum dolor sit amet consectetur adipisicing elit.
               Obcaecati cum nihil corporis exercitationem, Sit asperiores in
               praesentium qui quo aliquid natus expedita accusantium ipsum.
            </ServiceItem>
         </div>
      </section>
      <section class="Section Section-3">
         <h1>Notable Partners</h1>
         <div class="Carousel-Container">
            <div v-for="(_, index) in 2" :key="index" class="Partners-Carousel">
               <Partner :src="Jumia" alt="Jumia" />
               <Partner :src="Amazon" alt="Amazon" />
               <Partner :src="Konga" alt="Konga" />
               <Partner :src="Etsy" alt="Etsy" />
               <Partner :src="Ebay" alt="Ebay" />
               <Partner :src="Macys" alt="Macy's" />
            </div>
         </div>
      </section>
   </main>
</template>

<style scoped>
.App-Services {
   margin-top: var(--Header-Size);
}
.Section-1 {
   display: flex;
   flex-direction: row;
   justify-content: center;
   align-items: center;
   flex-direction: column;
   background: linear-gradient(105.76deg, #11567d 6.99%, #174552 85.54%);
}
.Section-1 .Heading {
   color: #c1dbe4;
   background-clip: unset;
   -webkit-background-clip: unset;
   -webkit-text-fill-color: unset;
   background: none;
}
.Section-1 .Line {
   width: 75%;
   height: 7px;
   background-color: #c1dbea;
   border-radius: 10px;
}
.Section-1 .Paragraph {
   width: 65%;
   font-style: normal;
   font-weight: 700;
   font-size: 20.4848px;
   line-height: 27px;
   text-align: center;
   letter-spacing: 0.01em;
   color: #c1dbe4;
}
.Section-2 {
   display: flex;
   justify-content: center;
   align-items: center;
}
.Grid-Container {
   margin-top: 300px;
   display: grid;
   grid: repeat(2, auto) / repeat(3, auto);
   row-gap: 25px;
   place-items: center;
}
.Section-3 {
   padding-right: 0;
   max-height: 450px;
}
.Section-3 h1 {
   margin-bottom: 35px;
}
.Carousel-Container {
   display: flex;
   width: 100%;
   overflow-x: hidden;
   border-left: 2px solid var(--Dark-Green);
}
.Partners-Carousel {
   display: flex;
   animation: scroll 50000ms infinite linear;
}
@keyframes scroll {
   100% {
      transform: translate(-100%);
   }
}
@media (max-width: 1024px) {
   .Grid-Container {
      row-gap: 50px;
   }
}
@media (max-width: 768px) {
   .Section-2 {
      justify-content: flex-start;
      align-items: flex-start;
      height: fit-content;
      max-height: fit-content;
      padding-top: 90px;
      margin-bottom: 39px;
   }
   .Grid-Container {
      display: flex;
      align-items: center;
      flex-direction: column;
      height: fit-content;
      max-height: fit-content;
   }
}
@media (max-width: 475px) {
   .Section-1 .Paragraph {
      font-size: 15px;
      line-height: 25px;
      width: 90%;
   }
}
</style>
