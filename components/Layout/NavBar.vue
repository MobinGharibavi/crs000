<template>
  <Body :class="{ 'overflow-hidden': sideMenu }">
    <div class="p-5 md:px-10 hidden lg:flex justify-between items-center">
      <NuxtLink
        :to="`/${locale}`"
        class="flex font-bold text-3xl rtl:flex-row-reverse"
      >
        <span class="text-orange-500">C</span>
        <p>rs</p>
        <span class="text-orange-500">T</span>
        <p>rip</p>
        <span class="text-orange-500">.</span>
      </NuxtLink>

      <div class="flex items-center gap-5">
        <NuxtLink :to="`/${locale}`"> {{ $t("navBar.home") }} </NuxtLink>
        <NuxtLink :to="`/${locale}`" class="text-gray-400">
          {{ $t("navBar.contact") }}
        </NuxtLink>
        <NuxtLink :to="`/${locale}`" class="text-gray-400">
          {{ $t("navBar.about") }}
        </NuxtLink>
      </div>

      <div
        class="flex p-1 h-[2.5rem] bg-[#F7F7F9] rounded-[0.5rem] min-w-[13.25rem] text-xs text-[#514037] mobile:hidden"
      >
        <div
          :class="{ 'text-orange bg-white': locale == 'fa' }"
          @click="handleRtlProject('fa')"
          class="w-1/3 grow cursor-pointer flex items-center justify-center rounded-[0.5rem]"
        >
          فارسی
        </div>
        <div
          @click="handleRtlProject('ar')"
          :class="{ 'text-orange bg-white': locale == 'ar' }"
          class="w-1/3 grow cursor-pointer flex items-center justify-center rounded-[0.5rem]"
        >
          عربی
        </div>
        <div
          @click="handleLtrProject('en')"
          :class="{ 'text-orange bg-white': locale == 'en' }"
          class="w-1/3 grow cursor-pointer flex items-center justify-center rounded-[0.5rem]"
        >
          English
        </div>
      </div>
    </div>

    <div class="flex px-10 py-5 lg:hidden justify-between">
      <TransitionSlide>
        <LayoutSideMenu v-if="sideMenu" @side="(data) => (sideMenu = data)" />
      </TransitionSlide>
      <button>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1.5rem"
          height="1.5rem"
          viewBox="0 0 14 14"
        >
          <path
            fill="currentColor"
            fill-rule="evenodd"
            d="M6.987 1.5A3.18 3.18 0 0 0 3.75 4.628V9a1 1 0 0 1-1 1H1.5A1.5 1.5 0 0 1 0 8.5v-2A1.5 1.5 0 0 1 1.5 5h.75v-.39A4.68 4.68 0 0 1 7 0a4.68 4.68 0 0 1 4.75 4.61V5h.75A1.5 1.5 0 0 1 14 6.5v2a1.5 1.5 0 0 1-1.5 1.5h-.75v.5a2.75 2.75 0 0 1-2.44 2.733A1.5 1.5 0 0 1 8 14H6.5a1.5 1.5 0 0 1 0-3H8c.542 0 1.017.287 1.28.718a1.25 1.25 0 0 0 .97-1.218V4.627A3.18 3.18 0 0 0 6.987 1.5"
            clip-rule="evenodd"
          />
        </svg>
      </button>

      <NuxtLink :to="`/${locale}`" class="text-orange font-bold text-xl">
        CRSTRIP
      </NuxtLink>

      <button @click="sideMenu = !sideMenu">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1.5rem"
          height="1.5rem"
          viewBox="0 0 24 24"
        >
          <path
            fill="currentColor"
            fill-rule="evenodd"
            d="M20.75 7a.75.75 0 0 1-.75.75H4a.75.75 0 0 1 0-1.5h16a.75.75 0 0 1 .75.75m0 5a.75.75 0 0 1-.75.75H4a.75.75 0 0 1 0-1.5h16a.75.75 0 0 1 .75.75m0 5a.75.75 0 0 1-.75.75H4a.75.75 0 0 1 0-1.5h16a.75.75 0 0 1 .75.75"
            clip-rule="evenodd"
          />
        </svg>
      </button>
    </div>
  </Body>
</template>

<script setup>
const { setLocale, locale } = useI18n();
const handleRtlProject = (lang) => {
  setLocale(lang);
  document.documentElement.setAttribute("dir", "rtl");
  document.documentElement.setAttribute("lang", lang);
};
const handleLtrProject = (lang) => {
  setLocale(lang);
  document.documentElement.setAttribute("dir", "ltr");
  document.documentElement.setAttribute("lang", lang);
};

const sideMenu = ref(false);
</script>
