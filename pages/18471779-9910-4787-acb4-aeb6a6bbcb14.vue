<template>
    <div class="sm:py-24 text-slate-800 overflow-hidden">
        <div class="my-24 flex justify-center">
            <icon class="text-2xl sm:text-6xl flex justify-items-center" icon="bxs:chevrons-down"></icon>
        </div>
        <h2 class="mb-3 sm:mb-6 text-2xl sm:text-5xl font-['Rubik_Glitch']">{{ doesnt }}</h2>
        <h2 class="mb-3 sm:mb-6 text-2xl sm:text-5xl font-['Rubik_Glitch']">{{ separator }}</h2>
        <h2 class="text-2xl sm:text-5xl font-['Rubik_Glitch']" v-html="does"></h2>
        <h1 class="my-12 sm:my-24 text-4xl sm:text-7xl font-['Jura'] animate__animated" v-html="newtech"
            v-intersection-observer="([{ isIntersecting }]) => { anima = isIntersecting }"
            :class="{ animate__fadeInRight: anima, animate__fadeOutRight: !anima, }"></h1>
        <div class="my-24 flex justify-center">
            <icon class="text-2xl sm:text-6xl flex justify-items-center" icon="bxs:chevrons-down"></icon>
        </div>
    </div>
    <ul class="divide-y-2 divide-dashed divide-slate-800" un-cloak>
        <li class="flex items-center gap-4 px-4 py-6 flex-nowrap" v-for="{ text, icon } in features">
            <div>
                <Icon :icon="icon" class="size-12" />
            </div>
            <el-text size="large" v-html="text"></el-text>
        </li>
    </ul>
</template>

<script setup>
import { ref } from "vue";
import { vIntersectionObserver } from "@vueuse/components";

const features = [
    { icon: "openmoji:rocket", text: "Create <a href='https://en.wikipedia.org/wiki/Static_web_page' target='_blank' class='underline hover:text-blue-800'>static websites</a> with <a href='https://vuejs.org' target='_blank' class='underline hover:text-blue-800'>Vue</a> without installing or setting up a development environment (<a href='https://nodejs.org' target='_blank' class='underline hover:text-blue-800'>Node.js</a>, <a href='https://vite.dev' target='_blank' class='underline hover:text-blue-800'>Vite</a>, etc.)" },
    { icon: "openmoji:building-construction", text: "Create <a href='https://vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>Vue single-file components</a> (also known as *.vue files, or SFC for Single File Component) without a preliminary build step" },
    { icon: "openmoji:racing-car", text: "Compilation of <a href='https://vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>Vue single-file components</a> occurs in the runtime mode directly in the browser when viewing the site, with no need for <a href='https://vuejs.org/guide/scaling-up/ssr.html' target='_blank' class='underline hover:text-blue-800'>SSR</a> (Server-Side Rendering)" },
    { icon: "openmoji:typescript", text: "Of course, you can use the <a href='https://vuejs.org/guide/introduction.html#composition-api' target='_blank' class='underline hover:text-blue-800'>Composition API</a>, moreover, it can be used together with <a href='https://vuejs.org/guide/typescript/composition-api.html' target='_blank' class='underline hover:text-blue-800'>TypeScript</a>" },
    { icon: "openmoji:spiral-notepad", text: "For static pages, use the <a href='https://en.wikipedia.org/wiki/WYSIWYG' target='_blank' class='underline hover:text-blue-800'>WYSIWYG</a> mode, which doesn’t require even basic knowledge of <a href='https://en.wikipedia.org/wiki/HTML' target='_blank' class='underline hover:text-blue-800'>HTML</a>" },
    { icon: "openmoji:code-editor", text: "For editing <a href='https://vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>Vue single-file components</a>, the <a href='https://microsoft.github.io/monaco-editor' target='_blank' class='underline hover:text-blue-800'>Monaco editor</a> is used (the same one as in <a href='https://code.visualstudio.com' target='_blank' class='underline hover:text-blue-800'>Microsoft VS Code</a>) with <a href='https://volarjs.dev' target='_blank' class='underline hover:text-blue-800'>Volar.js</a> pre-installed" },
    { icon: "openmoji:paintbrush", text: "Out of the box, the CSS framework <a href='https://tailwindcss.com' target='_blank' class='underline hover:text-blue-800'>Tailwind CSS</a> is supported; just use <a href='https://tailwindcss.com' target='_blank' class='underline hover:text-blue-800'>Tailwind CSS</a> classes without any additional configuration" },
    { icon: "openmoji:ship", text: "If you need external modules, such as libraries or frameworks, you can <a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import' target='_blank' class='underline hover:text-blue-800'>import</a> them, including directly from services like <a href='https://jsdelivr.com' target='_blank' class='underline hover:text-blue-800'>jsDelivr</a> and <a href='https://unpkg.com' target='_blank' class='underline hover:text-blue-800'>UNPKG</a>" },
    { icon: "openmoji:floppy-disk", text: "You can edit the website directly on your hard drive or connect to any S3 storage" },
    { icon: "openmoji:globe-with-meridians", text: "To run your website, you'll only need any basic <a href='https://en.wikipedia.org/wiki/Web_server' target='_blank' class='underline hover:text-blue-800'>web server</a> capable of serving static pages. In the case of S3, you don't even need that, as this functionality is usually built into the storage itself" },
    { icon: "openmoji:github", text: "By the way, <a href='https://docs.github.com/en/pages' target='_blank' class='underline hover:text-blue-800'>GitHub Pages</a> is also a great option for hosting your website—it works like a charm" },
    { icon: "openmoji:magnifying-glass-tilted-right", text: "Special attention is given to <a href='https://en.wikipedia.org/wiki/Search_engine_optimization' target='_blank' class='underline hover:text-blue-800'>search engine optimization</a> (SEO) mechanisms, which ensure that search bots can effectively index the site" },
    { icon: "openmoji:smiling-face-with-open-hands", text: "vueS3 is a non-commercial, <a href='https://en.wikipedia.org/wiki/Open-source_software' target='_blank' class='underline hover:text-blue-800'>open-source</a> project – feel free to explore and use it!" },
],
    doesnt = "Don't do it the old way",
    separator = "//",
    does = `Let's do <span class="text-white bg-red-500">&nbsp;everything differently&nbsp;</span>`,
    newtech = 'Try a <span class="text-white bg-slate-800">&nbsp;new technology&nbsp;</span> of website development',
    anima = ref(false);
</script>