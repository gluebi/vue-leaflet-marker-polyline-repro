<template>
    <div style="height: 100vh; width: 100vw">
        <l-map
            ref="map"
            v-model:zoom="zoom"
            :center="[53, 8]"
            :use-global-leaflet="true"
            :bounds="[53, 8]"
        >
            <l-tile-layer
                url="https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png"
                layer-type="base"
                name="OpenStreetMap"
            />
            <l-marker-cluster-group>
                <template v-for="item in 10">
                    <l-marker
                        :lat-lng="[53, 8]"
                        @popupopen="isVehiclePopupOpen = true"
                        @popupclose="isVehiclePopupOpen = false"
                    >
                        <l-popup> Popup </l-popup>
                    </l-marker>
                </template>
            </l-marker-cluster-group>
            <l-polyline
                v-if="isVehiclePopupOpen"
                :lat-lngs="[{ lat: 55, lng: 10 }, { lat: 56, lng: 11 }]"
                color="red"
            />
        </l-map>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, shallowRef, onMounted } from 'vue'
  import 'leaflet/dist/leaflet.css'
  // To be replaced by our own marker cluster styles
  import 'vue-leaflet-markercluster/dist/style.css'
  import { LMap, LTileLayer, LMarker, LPopup, LPolyline, LPolygon } from '@vue-leaflet/vue-leaflet'
  import L from 'leaflet'
  import { LMarkerClusterGroup } from 'vue-leaflet-markercluster'
  globalThis.L = L
  
  const isVehiclePopupOpen = ref<boolean>(false)
  const zoom = ref<number>(5)
  const map = ref<typeof LMap | null>(null)
  </script>
  