<template>
    <block>
        <div slot="title">{{ title }}</div>
        <div slot="description">{{ description }}</div>
        <div class="Block-samples" slot="content" v-html="markup"></div>
        <toggle slot="toggle">
            <markup language="markup" :code="markup"></markup>
        </toggle>
    </block>
</template>

<script>
import Block from '../../framework/organisms/Block'
import Toggle from '../../framework/molecules/Toggle.vue'
import Markup from '../../framework/atoms/Markup'

import '../../assets/scss/atoms/_unordered_lists.scss'

let markup = `
<ul class="UnorderedList">
    <li class="UnorderedList-item">List Item 1</li>
    <li class="UnorderedList-item">
        List Item 2
        <ul class="UnorderedList">
            <li class="UnorderedList-item">List Subitem 1</li>
            <li class="UnorderedList-item">List Subitem 2</li>
            <li class="UnorderedList-item">List Subitem 3</li>
        </ul>
    </li>
    <li class="UnorderedList-item">List Item 3</li>
    <li class="UnorderedList-item">List Item 4</li>
</ul>
`

export default {
    name: 'UnorderedLists',
    components: {
        Block,
        Toggle,
        Markup
    },
    data () {
        return {
            title: 'Unordered Lists',
            description: 'Some description',
            markup: markup
        }
    }
}
</script>

<style lang="scss">
</style>
