<template>
    <article class="examples__block">
        <h2 class="examples__block__title">
            USA SVG heat map with tooltips
        </h2>
        <div class="examples__block__map examples__block__map--usa">
            <Map :map="USA" :location-class="getLocationClass" @mouseover="pointLocation" @mouseout="unpointLocation"
                @mousemove="moveOnLocation" />
            <div class="examples__block__map__tooltip" :style="tooltipStyle">
                {{ pointedLocation }}
            </div>
        </div>
    </article>
</template>

<script>
import MAPS from 'svg-maps';
// import { getLocationName } from '../utilities'
import Map from './Map.vue'
export default {
    name: 'HeatMap',
    components: {
        Map,
    },
    data() {
        return {
            USA: MAPS.USA,
            pointedLocation: null,
            tooltipStyle: null,
        }
    },
    methods: {
        getLocationName(node) {
            return node && node.attributes.name.value
        },
        pointLocation(event) {
            this.pointedLocation = this.getLocationName(event.target)
        },
        unpointLocation(event) {
            this.pointedLocation = null
            this.tooltipStyle = { display: 'none' }
        },
        moveOnLocation(event) {
            this.tooltipStyle = {
                display: 'block',
                top: `${event.clientY + 10}px`,
                left: `${event.clientX - 100}px`,
            }
        },
        getLocationClass(location, index) {
            // Generate heat map
            return `svg-map__location svg-map__location--heat${index % 4}`
        },
    },
}
</script>