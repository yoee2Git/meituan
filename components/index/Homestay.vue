<template>
	<section class="m-has-style" @click='go'>
		<dl @mouseover="handleOver">
			<dt>民宿推荐</dt>
			<dd 
				:class="{active:kind==='all'}"
				kind="all"
				keyword="景点">
				全部
			</dd>
			<dd 
				:class="{active:kind==='date'}"
				kind="date"
				keyword="美食">
				约会聚餐
			</dd>
			<dd 
				:class="{active:kind==='spa'}"
				kind="spa"
				keyword="丽人">
				丽人SPA
			</dd>
			<dd 
				:class="{active:kind==='movie'}"
				kind="movie"
				keyword="电影">
				电影演出
			</dd>
			<dd 
				:class="{active:kind==='travel'}"
				kind="travel"
				keyword="旅游">
				品质出游
			</dd>
		</dl>
		<ul class="has-style-body">
			<li 
				v-for="item in curList" 
				:key="item.title">
				<el-card 
					:body-style="{ padding: '0px' }"
					shadow="never">
					<img :src="item.img"
								class="image" />
					<ul class="content-body">
						<li class="title">{{ item.title }}</li>
						<li class="pos"><span>{{ item.pos }}</span></li>
						<li class="price">￥<em>{{ item.price }}</em><span>/起</span></li>
					</ul>
				</el-card>
			</li>
		</ul>
	</section>
</template>

<script>
export default {
	name: 'Homestay',
	data() {
		return {
			kind: 'all',
			list: {
				all: [],
				date: [],
				spa: [],
				movie: [],
				travel: []
			}
		}
	},
	computed: {
		curList: function() {
			return this.list[this.kind]
		}
	},
	async mounted() {
		let { status, data: {count, pois}} = await this.$axios.get('/search/resultsByKeywords', {
			params: {
				keyword: '景点',
				city: this.$store.state.geo.position.city
			}
		})

		if (status === 200 && count > 0) {
			let res = pois.filter(item => item.photos.length).map(item => {
				return {
					title: item.name,
					pos: item.type.split(';')[0],
					price: item.biz_ext.cost || '暂无',
					img: item.photos[0].url,
					url: '//aaa.com'
				}
			})
			this.list[this.kind] = res.slice(0, 9);
		} else {
			this.list[this.kind] = [];
		}
	},
	methods: {
    go(){
      this.$router.push('products')
    },
		handleOver: async function(e) {
			let dom = e.target;
			let tag = dom.tagName.toLowerCase();
			if (tag === 'dd') {
				this.kind = dom.getAttribute('kind');
				let keyword = dom.getAttribute('keyword');

				let { status, data: {count, pois}} = await this.$axios.get('/search/resultsByKeywords', {
					params: {
						keyword,
						city: this.$store.state.geo.position.city
					}
				})

				if (status === 200 && count > 0) {
					let res = pois.filter(item => item.photos.length).map(item => {
						return {
							title: item.name,
							pos: item.type.split(';')[0],
							price: item.biz_ext.cost || '暂无',
							img: item.photos[0].url,
							url: '//aaa.com'
						}
					})
					this.list[this.kind] = res.slice(0, 9);
				} else {
					this.list[this.kind] = [];
				}
			}
		}
	}
}
</script>

<style lang="scss">
@import "@/assets/css/index/homestay.scss";
</style>
