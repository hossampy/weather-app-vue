 <template>
  <div class="flex flex-col min-h-screen font-Roboto bg-weather-primary">
    <site-navigation></site-navigation>
    <router-view> </router-view> 
  </div>
</template>

<script>
import { RouterView } from 'vue-router';
import SiteNavigation from './components/SiteNavigation.vue';

export default {
  components: {
    RouterView,
    SiteNavigation
  }
}
</script> 
 
 <!--  <template>
  <div> <site-navigation> </site-navigation>
  <router-view> </router-view>
  <RouterView />  
</div>
  
</template>

<script>
import { RouterView } from 'vue-router'; 
import SiteNavigation from './components/SiteNavigation.vue';
export default {
components:{ 
 
SiteNavigation
}
}
</script>

<style>

</style>  -->
