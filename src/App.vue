<template>
    <div id="app">
        <div class="container" v-cloak>
            <div class="well well-sm">
                <div class="pull-left">
                    <a class="github-button" href="https://github.com/sohrabtaee/standard-persian-fonts" data-size="large" aria-label="Star sohrabtaee/standard-persian-fonts on GitHub">Star on Github</a>
                </div>
                <p>                    در صورتی که فونت فارسی استانداری می‌شناسید که در این لیست وجود ندارد، فونت مورد نظر را به ایمیل من بفرستید.</p>
                <a href="mailto:&#115;&#111;&#104;&#114;&#097;&#098;&#046;&#116;&#097;&#101;&#101;&#064;&#103;&#109;&#097;&#105;&#108;&#046;&#099;&#111;&#109;">&#115;&#111;&#104;&#114;&#097;&#098;&#046;&#116;&#097;&#101;&#101;&#064;&#103;&#109;&#097;&#105;&#108;&#046;&#099;&#111;&#109;</a>
            </div>
            <div class="row">
                <div class="col-sm-7 col-md-8 col-lg-9">
                    <div class="panel panel-default" v-for="font in filteredFonts" :key="font.nameEn"
                         :class="font.nameEn | slug">
                        <div class="panel-heading clearfix">
                            <h3 class="pull-right panel-title">{{font.nameFa}} ({{font.nameEn}})</h3>
                            <h3 class="pull-left panel-title" v-if="font.url">
                                <a :href="font.url" target="_blank">صفحه سازنده</a>
                            </h3>
                        </div>
                        <div class="row">
                            <div :class="font.weights.length > 1 ? 'col-lg-6' : 'col-xs-12'"
                                 v-for="weight in font.weights">
                                <div class="panel-body" :class="weight">
                                    <p>یکی از مشکلاتی که در وب فارسی با آن مواجه هستیم، محدودیت فونت است. متاسفانه
                                        در وب
                                        فارسی ما
                                        محدود به سه فونت هستیم
                                        که بر روی تمامی سیستم ها نصب شده است. فونت arial, Tahoma و mono-type تنها
                                        فونتهایی هستند که
                                        می‌توانیم از آنها
                                        استفاده کنیم در حالی که برای زبان انگلیسی حداقل نزدیک به 10 فونت در دسترس
                                        است.</p>
                                    <div class="numbers">
                                        <p>1 2 3 4 5 6 7 8 9 0 - = ! @ # $ % ^ & * ( ) _ +</p>
                                        <p>۱ ۲ ۳ ۴ ۵ ۶ ۷ ۸ ۹ ۰ - = ! ٬ ٫ ریال ٪ × ، * ) ( ـ +</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-sm-5 col-md-4 col-lg-3">
                    <div class="panel panel-default">
                        <div class="panel-heading clearfix">
                            <h4 class="panel-title">فیلتر</h4>
                        </div>
                        <div class="panel-body">
                            <label>بر اساس نوع فونت</label>
                            <div class="checkbox">
                                <label>
                                    <input type="checkbox" value="sans-serif"
                                           @click="filter" v-model="filters.types"> لبه گرد (sans-serif)
                                </label>
                            </div>
                            <div class="checkbox">
                                <label>
                                    <input type="checkbox" value="serif"
                                           @click="filter" v-model="filters.types"> لبه تیز (serif)
                                </label>
                            </div>
                        </div>
                        <div class="panel-body">
                            <label>بر اساس وزن فونت</label>
                            <div class="checkbox" v-for="weight in weights">
                                <label>
                                    <input type="checkbox" :value="weight | slug"
                                           @click="filter" v-model="filters.weights"> {{weight}}
                                </label>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Includes from 'lodash/includes';
    import Difference from 'lodash/difference';

    export default {
        name: 'app',
        data () {
            return {
                weights: ['Ultra light', 'Light', 'Normal', 'Medium', 'Bold', 'Black'],
                filters: {
                    types: [],
                    weights: []
                },
                filteredFonts: [],
                fonts: [
                    {
                        nameFa: 'بی‌بی‌سی نسیم',
                        nameEn: 'BBC Nassim',
                        url: 'https://www.rosettatype.com/custom-fonts/BBC-Nassim',
                        type: 'serif',
                        weights: ['normal', 'bold']
                    },
                    {
                        nameFa: 'دروید نسخ',
                        nameEn: 'Droid Naskh',
                        url: 'https://fontlibrary.org/en/font/droid-arabic-naskh',
                        type: 'serif',
                        weights: ['normal', 'bold']
                    },
                    {
                        nameFa: 'گندم',
                        nameEn: 'Gandom',
                        url: 'https://github.com/rastikerdar/gandom-font',
                        type: 'serif',
                        weights: ['normal', 'bold']
                    },
                    {
                        nameFa: 'گنج نامه',
                        nameEn: 'Ganj Nameh',
                        url: 'https://github.com/font-store/GanjnamehFont',
                        type: 'sans-serif',
                        weights: ['normal']
                    },
                    {
                        nameFa: 'ایران سنس',
                        nameEn: 'Iran Sans',
                        url: 'http://fontiran.com/%D8%AE%D8%A7%D9%86%D9%88%D8%A7%D8%AF%D9%87-%D9%81%D9%88%D9%86%D8%AA-%D8%A7%DB%8C%D8%B1%D8%A7%D9%86-%D8%B3%D9%86-%D8%B3%D8%B1%DB%8C%D9%81-iran-sans-%D9%BE%D9%86%D8%AC-%D9%88%D8%B2%D9%86-%D9%87%D9%85/',
                        type: 'sans-serif',
                        weights: ['ultra-light', 'light', 'normal', 'medium', 'bold']
                    },
                    {
                        nameFa: 'ایران یکان',
                        nameEn: 'Iran Yekan',
                        url: 'http://fontiran.com/%D9%81%D9%88%D9%86%D8%AA-%D8%A7%DB%8C%D8%B1%D8%A7%D9%86-%DB%8C%DA%A9%D8%A7%D9%86-iran-yekan/',
                        type: 'sans-serif',
                        weights: ['light', 'normal', 'bold']
                    },
                    {
                        nameFa: 'میلاد آزاد',
                        nameEn: 'Milad Azad',
                        url: 'https://github.com/font-store/font-MiladAzad',
                        type: 'serif',
                        weights: ['normal']
                    },
                    {
                        nameFa: 'پرستو',
                        nameEn: 'Parastoo',
                        url: 'https://github.com/rastikerdar/parastoo-font',
                        type: 'serif',
                        weights: ['normal', 'bold']
                    },
                    {
                        nameFa: 'ساحل',
                        nameEn: 'Sahel',
                        url: 'https://github.com/rastikerdar/sahel-font',
                        type: 'sans-serif',
                        weights: ['normal', 'bold', 'black']
                    },
                    {
                        nameFa: 'صمیم',
                        nameEn: 'Samim',
                        url: 'https://github.com/rastikerdar/samim-font',
                        type: 'sans-serif',
                        weights: ['normal', 'bold']
                    },
                    {
                        nameFa: 'شبنم',
                        nameEn: 'Shabnam',
                        url: 'https://github.com/rastikerdar/shabnam-font',
                        type: 'sans-serif',
                        weights: ['normal', 'bold']
                    },
                    {
                        nameFa: 'وزیر',
                        nameEn: 'Vazir',
                        url: 'https://github.com/rastikerdar/vazir-font',
                        type: 'sans-serif',
                        weights: ['ultra-light', 'normal', 'medium', 'bold']
                    },
                    {
                        nameFa: 'ویژه آزاد',
                        nameEn: 'Vizheh Azad',
                        url: 'https://github.com/font-store/font-VizhehAzad',
                        type: 'serif',
                        weights: ['normal']
                    },
                    {
                        nameFa: 'زیرو سنس',
                        nameEn: 'Xero Sans',
                        url: '',
                        type: 'sans-serif',
                        weights: ['normal']
                    }
                ]
            }
        },
        mounted() {
            this.filteredFonts = this.fonts;
        },
        methods: {
            filter () {
                this.filteredFonts = this.fonts;
                if (this.filters.types.length) {
                    this.filteredFonts = this.filteredFonts.filter(font => Includes(this.filters.types, font.type));
                }
                if (this.filters.weights.length) {
                    this.filteredFonts = this.filteredFonts.filter(font => !Difference(this.filters.weights, font.weights).length);
                }
            }
        },
        filters: {
            slug(value) {
                return value.replace(/\s+/g, '-').toLowerCase();
            }
        }
    }
</script>

<style>
    @import "css/bootstrap.min.css";
    @import "css/bootstrap-rtl.min.css";
    @import "css/font-face.scss";

    html {
        font-size: 16px;
    }

    body {
        direction: rtl;
        font-family: 'Iran Sans', sans-serif;
        font-size: 1rem;
        line-height: 1.8;
    }

    .numbers {
        text-align: center;
        direction: ltr;
    }

    [v-cloak] {
        display: none;
    }

    #app {
        padding-top: 3em;
    }

    .well p {
        margin: 0;
    }

    .panel {
        margin-bottom: 2em;
    }

    .panel-title {
        white-space: nowrap;
    }

    .panel-title a {
        color: #337ab7;
    }

    .panel-title a:hover {
        color: #23527c;
    }

    .ultra-light {
        font-weight: 200;
    }

    .light {
        font-weight: 300;
    }

    .medium {
        font-weight: 500;
    }

    .bold {
        font-weight: 700;
    }

    .black {
        font-weight: 900;
    }
</style>
