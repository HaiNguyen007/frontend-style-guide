<template>
    <block>
        <div slot="title">{{ title }}</div>
        <div slot="description">{{ description }}</div>
        <div class="Block-samples" slot="content">
            <div class="Colors">
                <div class="Colors-section" v-for="section in colors">
                    <h2 class="Colors-title">{{ section.title }}</h2>
                    <ul class="Colors-list">
                        <li class="Colors-item" v-for="color, key in section.colors">
                            <div class="Colors-sample" :style="'background:' + color"></div>
                            <div class="Colors-info">
                                <span class="Colors-code">$c-{{ key }}</span>
                                <span class="Colors-hex">{{ color }}</span>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
        <tabs slot="tabs">
            <tab slot="tab" label="Sass Variables" selected>
                <markup slot="tabContent" language="scss" :code="colorsSass().vars"></markup>
            </tab>
            <tab slot="tab" label="Sass Class Array">
                <markup slot="tabContent" language="scss" :code="colorsSass().arr"></markup>
            </tab>
            <tab slot="tab" label="Sass Class Helpers">
                <markup slot="tabContent" language="scss" :code="helpers"></markup>
            </tab>
        </tabs>
    </block>
</template>

<script>
import Tab from '../../framework/atoms/Tab.vue'
import Markup from '../../framework/atoms/Markup'
import Tabs from '../../framework/molecules/Tabs.vue'
import Toggle from '../../framework/molecules/Toggle.vue'
import Block from '../../framework/organisms/Block'

import '../../assets/scss/atoms/_colors.scss'
import colors from '../../data/colors.js'

const helpers = `
@each $name, $color in $colors {
    .c-#{$name} { color: #{$color}; }
    .bg-#{$name} { background: #{$color}; }

    .c-hover-#{$name}:hover {
        @include breakpoint($s768) {
            color: #{$color};
        }
    }

    .bg-hover-#{$name}:hover {
        @include breakpoint($s768) {
            background: #{$color};
        }
    }
}
`

export default {
    name: 'Colors',
    components: {
        Block,
        Toggle,
        Markup,
        Tabs,
        Tab
    },
    data () {
        return {
            title: 'Colors',
            description: '',
            colors: colors,
            helpers: helpers
        }
    },
    methods: {
        colorsSass: function () {
            let arr = '$colors:'
            let vars = ''

            Object.keys(colors).forEach(function (key) {
                Object.keys(colors[key].colors).forEach(function (name, index) {
                    arr += `
    (${name}, $c-${name})`
                    vars += `
    $c-${name}: ${colors[key].colors[name]};`
                });
            });

            return {
                vars: vars,
                arr: arr
            }
        }
    }
}
</script>

<style lang="scss">
</style>
