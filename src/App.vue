<script setup>
const base = import.meta.env.BASE_URL;

// 報名連結（只保留最後一頁的按鈕導向此處）
const signupUrl =
  "https://www.instagram.com/allstar_xs?utm_source=ig_web_button_share_sheet&igsh=ZDNlZDc0MzIxNw==";

// 每一頁 = 一張圖片。
// covers：用深色色塊蓋掉圖片中已烘焙進去、要「移除」的報名按鈕。
// link：透明可點擊熱區，導向報名連結（只有最後一頁有）。
// 座標皆為相對於該張圖片的百分比，會隨圖片縮放；若需微調直接改這裡。
const pages = [
  {
    src: `${base}1.jpg`,
    alt: "UNO 大賽 x XS 能量飲料",
    covers: [
      // 底部「立即報名 >>>」橫條
      { top: "75.5%", left: "2%", width: "96%", height: "9.5%" },
    ],
    link: null,
  },
  {
    src: `${base}2.jpg`,
    alt: "XS 能量飲料系列介紹",
    covers: [
      // 整列導覽列（活動介紹／賽制說明…＋右上立即報名）
      { top: "0%", left: "0%", width: "100%", height: "5.5%" },
      // 底部「立即報名參加 >」
      { top: "90%", left: "10%", width: "80%", height: "9%" },
    ],
    link: null,
  },
  {
    src: `${base}3.jpg`,
    alt: "XS 的故事",
    covers: [
      // 整列導覽列（活動介紹／賽制說明…＋右上立即報名）
      { top: "0%", left: "0%", width: "100%", height: "5.5%" },
    ],
    link: null,
  },
  {
    src: `${base}4.jpg`,
    alt: "XS 全口味介紹",
    covers: [
      // 整列導覽列（活動介紹／賽制說明…＋右上立即報名）
      { top: "0%", left: "0%", width: "100%", height: "5.5%" },
      // 底部「立即報名參加 >」
      { top: "90%", left: "14%", width: "72%", height: "9%" },
    ],
    link: null,
  },
  {
    src: `${base}5.jpg`,
    alt: "賽制",
    covers: [{ top: "0%", left: "0%", width: "100%", height: "5.5%" }],
    link: null,
  },
  {
    src: `${base}6.jpg`,
    alt: "活動辦法",
    covers: [
      // 整列導覽列（移除，只保留下方主按鈕）
      { top: "0%", left: "0%", width: "100%", height: "5.5%" },
    ],
    // 底部「立即報名」主按鈕：保留並導向報名連結
    link: { top: "89.5%", left: "14%", width: "72%", height: "7%" },
  },
];
</script>

<template>
  <div class="min-h-screen bg-black">
    <div class="mx-auto w-full max-w-[640px]">
      <div v-for="(page, i) in pages" :key="i" class="relative">
        <img :src="page.src" :alt="page.alt" class="block w-full align-top" />

        <!-- 蓋掉要移除的報名按鈕 -->
        <span
          v-for="(c, ci) in page.covers"
          :key="ci"
          class="pointer-events-none absolute bg-black"
          :style="{
            top: c.top,
            left: c.left,
            width: c.width,
            height: c.height,
          }"
        />

        <!-- 可點擊報名熱區（僅最後一頁） -->
        <a
          v-if="page.link"
          :href="signupUrl"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="立即報名"
          class="absolute block cursor-pointer"
          :style="{
            top: page.link.top,
            left: page.link.left,
            width: page.link.width,
            height: page.link.height,
          }"
        />
      </div>
    </div>
  </div>
</template>
