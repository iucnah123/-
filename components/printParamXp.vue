<template>
	<view class="param">
		<text class="param-title">打印参数设置</text>
		<view v-if="showParam.indexOf(1) != -1" class="color">
			<text class="color-title">颜色</text>
			<view class="color-select">
				<view @click="color = 0" :class="color == 0 ? 'active' : ''">黑白</view>
				<view @click="color = 1" :class="color == 1 ? 'active' : ''">彩色</view>
			</view>
		</view>
		<view v-if="showParam.indexOf(2) != -1" class="color">
			<text class="color-title">版面</text>
			<view class="color-select">
				<view @click="sides = 0" :class="sides == 0 ? 'active' : ''">单面</view>
				<view @click="sides = 1" :class="sides == 1 ? 'active' : ''">双面</view>
			</view>
		</view>
		<view v-if="showParam.indexOf(3) != -1" class="pages">
			<text class="pages-title">份数</text>
			<view class="pages-counter">
				<view @click="counter('printNum', -1)">-</view>
				<input disabled="true" v-model="printNum" />
				<view @click="counter('printNum', 1)">+</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: 'footerCount',
	props: {
		showParam: {
			type: Array,
			default: () => [1, 2, 3]
		}
	},
	data: () => ({
		//颜色 1 彩色 0 黑白
		color: 1,
		//单双面 1 双面 0 单面
		sides: 0,
		//打印份数
		printNum: 1
	}),
	methods: {
		counter(field, val) {
			if (this[field] + val <= 0) {
				return;
			}
			this[field] += val;
		}
	},
	computed: {
		color() {
			return this.color;
		},
		sides() {
			return this.sides;
		},
		printNum() {
			return this.printNum;
		}
	},
	watch: {
		color(val) {
			uni.$emit('picPrintParamChange', { field: 'color', val: val });
		},
		sides(val) {
			uni.$emit('picPrintParamChange', { field: 'sides', val: val });
		},
		printNum(val) {
			uni.$emit('picPrintParamChange', { field: 'printNum', val: val });
		}
	}
};
</script>

<style lang="scss">
.param {
	padding: 40upx 27upx;
	background: $color-ff;
	border-radius: 30upx;
	& .param-title {
		@include font-no-height(24upx, 500, $color-99);
	}
	& .color {
		@include display-flex-space-between;
		margin-top: 28upx;
		& .color-title {
			@include font-no-height(32upx, 400, $color-33);
		}
		& .color-select {
			@include display-flex-start;
			view {
				width: 100upx;
				height: 54upx;
				display: flex;
				justify-content: center;
				align-items: center;
				@include font-no-height(24upx, 500, $color-A2A3A3);
			}
			view:nth-child(1) {
				border-radius: 27upx 0px 0px 27upx;
				border-top: 3upx solid $color-DC;
				border-left: 3upx solid $color-DC;
				border-bottom: 3upx solid $color-DC;
			}
			view:nth-child(2) {
				border-radius: 0px 27upx 27upx 0px;
				border-top: 3upx solid $color-DC;
				border-right: 3upx solid $color-DC;
				border-bottom: 3upx solid $color-DC;
			}
			& .active {
				border: 3upx solid $color-3985FF;
				background: $color-3985FF;
				@include font-no-height(24upx, 500, $color-ff !important);
			}
		}
	}
	& .pages {
		@include display-flex-space-between;
		margin-top: 28upx;
		& .pages-title {
			@include font-no-height(32upx, 400, $color-33);
		}
		& .pages-counter {
			@include display-flex-start;
			view {
				@include w-h(70upx, 54upx);
				display: flex;
				justify-content: center;
				align-content: center;
				border: 3upx solid $color-C5;
				color: $color-C5;
			}
			view:nth-child(1) {
				border-radius: 27upx 0px 0px 27upx;
			}
			view:nth-child(3) {
				border-radius: 0px 27upx 27upx 0px;
			}
			input {
				@include w-h(60upx, 54upx);
				@include font-no-height(24upx, 500, $color-3985FF);
				border-top: 3upx solid $color-DC;
				border-bottom: 3upx solid $color-DC;
				text-align: center;
			}
		}
	}
}
</style>
