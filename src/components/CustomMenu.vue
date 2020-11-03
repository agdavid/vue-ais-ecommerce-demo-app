<template>
    <div>
        <label>Custom Menu</label>
        <ul v-if="state">
            <li v-for="item in items" :key="item.value">
                <button @click="state.refine(item.value)">
                    {{ item.label }}
                </button>
            </li>
        </ul>
    </div>
</template>

<script>
import { createWidgetMixin } from 'vue-instantsearch';
import { connectMenu } from 'instantsearch.js/es/connectors';

export default {
    mixins: [
        createWidgetMixin({ connector: connectMenu })
    ],
    props: {
        attribute: {
        type: String,
        required: true,
        },
    },
    computed: {
        widgetParams() {
            return {
                attribute: this.attribute,
            };
        },
        items() {
            const updatedItems = this.state.items.map( item => {
                if (item.label.toLowerCase().includes('phone')) {
                    item.label = `${item.label} + 📞`;
                }
                return item;
            })
            return updatedItems;
        },
    }
}
</script>