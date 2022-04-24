<template>
	<div>
		<vueWaterfallEasy ref="waterfall" srcKey="avatar_url" hrefKey="html_url" :imgsArr="imgsArr" @scrollReachBottom="getData">
			<div slot="waterfall-head">
				<Search />
			</div>
			<div class="imginfo" slot-scope="props">
				<p class="someinfo">{{ props.value.login }}</p>
			</div>
			<div slot="waterfall-over">已全部加载完毕(●'◡'●)</div>
		</vueWaterfallEasy>
	</div>
</template>

<script>
import Search from './Search';
import axios from 'axios';
import vueWaterfallEasy from 'vue-waterfall-easy';
export default {
	name: 'List',
	components: { vueWaterfallEasy, Search },
	data() {
		return {
			imgsArr: [],
			group: 0,
			scrollTop: 0
		};
	},
	mounted() {
		// this.getData()
	},
	methods: {
		getData() {
			this.group++;
			if (this.group === 4) {
				this.$refs.waterfall.waterfallOver();
				return;
			}
			axios.get(`https://api.github.com/search/users?q=o&page=${this.group}&per_page=20`).then(
				(res) => {
					let imgda = res.data.items;
					imgda.forEach((item) => {
						this.imgsArr.push({
							avatar_url: item.avatar_url,
							html_url: item.html_url,
							login: item.login
						});
					});
				},
				(error) => {}
			);
		}
	}
};
</script>
<style lang="less" scoped>
// 显示瀑布流的图片数据
.vue-waterfall-easy-container {
	overflow-y: hidden !important;
	height: 100% !important;
	position: fixed !important;
}
.vue-waterfall-easy-scroll {
	overflow-y: hidden !important;
}
.imginfo {
	text-align: center;
	text-decoration: none !important;
}
.someinfo {
	text-align: center;
	text-decoration: none !important;
}
</style>
