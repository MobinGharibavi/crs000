<template>
  <section class="py-4 bg-white rounded-xl mt-5">
    <ClientOnly>
      <Carousel
        :loop="true"
        :wrapAround="true"
        :autoplay="2500"
        :breakpoints="breakpoints"
      >
        <Slide v-for="(item, index) in date" :key="index">
          <div class="swiper-slide">
            <label
              class="select flex-col rounded-lg text-center border border-transparent transition-all hover:bg-orange-100 hover:border-[#ff5a00] hover:text-[#ff5a00] w-[129px] h-14 cursor-pointer text-sm text-[#1D1B20] flex items-center justify-center"
              :class="{
                '!text-[#ff5a00] !border-[#ff5a00] !bg-orange-100':
                  correctISO(`${item.date}/${new Date().getFullYear()}`) ===
                  openTab,
              }"
            >
              <input
                type="radio"
                v-model="openTab"
                :value="correctISO(`${item.date}/${new Date().getFullYear()}`)"
                @click="
                  changeDate(
                    correctISO(`${item.date}/${new Date().getFullYear()}`)
                  )
                "
                :checked="
                  correctISO(`${item.date}/${new Date().getFullYear()}`) ===
                  openTab
                "
                class="hidden"
              />
              <span class="text">{{ item.date }}</span>
              <span class="font-semibold">{{ item.day }}</span>
            </label>
          </div>
        </Slide>
      </Carousel>
    </ClientOnly>
  </section>
</template>

<script setup>
import { addDay, format } from "@formkit/tempo";
const { execute } = defineProps({
  execute: Function,
});
const breakpoints = ref({
  400: {
    itemsToShow: 3,
  },
  576: {
    itemsToShow: 5,
  },
  768: {
    itemsToShow: 7,
  },
  992: {
    itemsToShow: 8,
  },
  1200: {
    itemsToShow: 9,
  },
});
const router = useRouter();
const route = useRoute();
const openTab = ref(route.query.departure_date_time);

const { locale } = useI18n();
const date = ref([]);

for (let i = 0; i < 20; i++) {
  if (locale.value == "en") {
    const tt = format(addDay(new Date().toISOString(), i), "ddd", locale.value);
    const dd = format(
      addDay(new Date().toISOString(), i),
      "MM/DD",
      locale.value
    );
    date.value.push({
      day: tt,
      date: dd,
    });
  } else {
    const tt = format(
      addDay(new Date().toISOString(), i),
      "dddd",
      locale.value
    );
    const dd = format(
      addDay(new Date().toISOString(), i),
      "MM/DD",
      locale.value
    );
    date.value.push({
      day: tt,
      date: dd,
    });
  }
}

const correctISO = (time) => {
  const changeTime = time.replace(/[۰-۹]/g, (d) => '۰۱۲۳۴۵۶۷۸۹'.indexOf(d));
  const [month, day, year] = changeTime.split("/").map(Number);
  const date = new Date(year, month - 1, day);
  date.setDate(date.getDate() + 1);
  return date.toISOString();
};

const changeDate = (date) => {
  openTab.value = date;
  router.push({
    path: `/${locale.value}/Filter`,
    query: {
      origin: route.query.origin,
      destination: route.query.destination,
      departure_date_time: date,
      return_date_time: route.query.return_date_time,
    },
  });
  execute();
};
</script>
