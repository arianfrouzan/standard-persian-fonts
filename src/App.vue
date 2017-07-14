<template>
    <div id="app">
        <div class="container" v-cloak>
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
                    <div class="panel panel-info">
                        <div class="panel-heading">
                            <a class="github-button" href="https://github.com/sohrabtaee/standard-persian-fonts" data-size="large" aria-label="Star sohrabtaee/standard-persian-fonts on GitHub">Star on Github</a>
                        </div>
                        <div class="panel-body">
                            <p>                    در صورتی که فونت فارسی استانداری می‌شناسید که در این لیست وجود ندارد، فونت مورد نظر را به ایمیل زیر بفرستید.</p>
                            <a href="mailto:&#115;&#111;&#104;&#114;&#097;&#098;&#046;&#116;&#097;&#101;&#101;&#064;&#103;&#109;&#097;&#105;&#108;&#046;&#099;&#111;&#109;">&#115;&#111;&#104;&#114;&#097;&#098;&#046;&#116;&#097;&#101;&#101;&#064;&#103;&#109;&#097;&#105;&#108;&#046;&#099;&#111;&#109;</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Fonts from './fonts';
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
                fonts: Fonts
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

    .panel-info {
        text-align: center;
        font-size: 85%;
    }

    .panel-info p {
        margin: 0 0 0.5em;
        color: grey;
    }

    .panel-info .panel-heading {
        font-size: 0;
    }

    .panel-title {
        white-space: nowrap;
        font-weight: normal;
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
