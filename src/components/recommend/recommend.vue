<template>
	<div class="recommend">
		<div class="recomment-content">
			<div v-if="recommends.length" class="slide-wrapper">
				<slider>
					<div v-for="item in recommends">
						<a :href="item.linkUrl">
							<img :src="item.picUrl">
						</a>
					</div>
				</slider>
			</div>
			<div class="recommend-list">
				<h1 class="list-title">热门歌单推荐</h1>
				<ul></ul>
			</div>
		</div>
	</div>
</template>

<script type="text/ecmascript-6">
	import {getRecommend} from 'api/recommend'
	import {ERR_OK} from 'api/config'
	import Slider from 'base/slider/slider'

	export default{
	  data () {
	    return {
	      recommends: []
	    }
	  },
	  // 生命周期
	  create () {
	    this._getRecommend()
	  },
	  methods: {
	    _getRecommend () {
	      getRecommend().then((res) => {
	        if (res.code === ERR_OK) {
	          this.recommends = res.data.slider
	        }
	      })
	    }
	  },
	  components: {
	    Slider
	  }
	}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
	.recommend{
	  position: fixed;
	  width: 100%;
	  top: 88px;
	  bottom: 0;
	}
	.recommend-list{
	  height: 100%;
	  overflow: hidden;
	}
	.slide-wrapper{
	  position: relative;
	  width: 100%;
	  overflow: hidden;
	}
	.recommend-list
	  .list-title
	    height: 65px;
	    line-height: 65px;
	    text-align: center;
	    font-size: $font-size-medium;
	    color: $color-theme;
	.item{
	  display: flex;
	  box-sizing: border-box;
	  align-items: center;
	  padding: 0 20px 20px 20px;
	}

</style>