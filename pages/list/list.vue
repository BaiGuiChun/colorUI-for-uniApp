<template>
	<view>
		<!-- <view class="cu-custom" style="height:{{CustomBar}}px;">
			<view class="cu-bar fixed bg-gradual-pink" style="height:{{CustomBar}}px;padding-top:{{StatusBar}}px;">
				<navigator class='action' open-type="navigateBack" delta="1" hover-class="none">
					<text class='icon-back'></text> 列表
				</navigator>
			</view>
		</view> -->
		<view class="cu-bar bg-white solid-bottom margin-top">
			<view class='action'>
				<text class='icon-title text-orange '></text> 宫格列表
			</view>
			<view class='action'>
				<button class='cu-btn bg-green shadow' @tap="showModal" :data-target="'gridModal'">设置</button>
			</view>
		</view>
		<view class="cu-modal" :class="modalName=='gridModal'?'show':''" @tap='hideModal'>
			<view class="cu-dialog" @click.stop>
				<radio-group class="block" @change="gridchange">
					<view class='cu-list menu text-left'>
						<view class='cu-item' v-for="(item,index) in 3" :key='index'>
							<label class='flex justify-between align-center flex-sub'>
								<view class='flex-sub'>{{index +3}} 列</view>
								<!-- <radio class='round' :value='index +3' :checked='gridCol==index+3'></radio> -->
							</label>
						</view>
					</view>
				</radio-group>
				<view class='cu-list menu text-left solid-top'>
					<view class='cu-item'>
						<view class='content'>
							<text class='text-grey'>边框</text>
						</view>
						<view class='action'>
							<switch @change="gridswitch"></switch>
						</view>
					</view>
				</view>
			</view>
		</view>

		<view class="cu-list grid" :class="[gridBorder?'':'no-border','col-'+gridCol]">
			<view class="cu-item" v-for="(item,index) in iconList" :key='index' v-if="index<gridCol*2">
				<view :class="['icon-'+item.icon,'text-'+item.color]">
					<view class="cu-tag badge" v-if="item.badge!=0">
						<block v-if="item.badge!=1">{{item.badge>99?'99+':item.badge}}</block>
					</view>
				</view>
				<text>{{item.name}}</text>
			</view>
		</view>


		<view class="cu-bar bg-white solid-bottom margin-top">
			<view class='action'>
				<text class='icon-title text-orange '></text> 菜单列表
			</view>
			<view class='action'>
				<button class='cu-btn bg-green shadow' @tap="showModal" :data-target="'menuModal'">设置</button>
			</view>
		</view>
		<view class="cu-modal" :class="modalName=='menuModal'?'show':''" @tap='hideModal'>
			<view class="cu-dialog" catchtap>
				<view class='cu-list menu text-left solid-top'>
					<view class='cu-item'>
						<view class='content'>
							<text class='text-grey'>短边框</text>
						</view>
						<view class='action'>
							<switch @change="menuBorders"></switch>
						</view>
					</view>
					<view class='cu-item'>
						<view class='content'>
							<text class='text-grey'>箭头</text>
						</view>
						<view class='action'>
							<switch @change="menuArrows"></switch>
						</view>
					</view>
					<view class='cu-item'>
						<view class='content'>
							<text class='text-grey'>卡片</text>
						</view>
						<view class='action'>
							<switch @change="menuCards"></switch>
						</view>
					</view>
				</view>
			</view>
		</view>

		<view class="cu-list menu" :class="[menuBorder?'sm-border':'',menuCard?'card-menu margin-top':'']">
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class='content'>
					<text class='icon-circlefill text-grey'></text>
					<text class='text-grey'>图标 + 标题</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class='content'>
					<image src='../../static/images/logo.png' class='png' mode='aspectFit'></image>
					<text class='text-grey'>图片 + 标题</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<button class='cu-btn content' open-type='contact'>
					<text class='icon-btn text-olive'></text>
					<text class='text-grey'>Open-type 按钮</text>
				</button>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<navigator class='content' hover-class='none' url='../list/list' open-type="redirect">
					<text class='icon-discoverfill text-orange'></text>
					<text class='text-grey'>Navigator 跳转</text>
				</navigator>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class='content'>
					<text class='icon-emojiflashfill text-pink'></text>
					<text class='text-grey'>头像组</text>
				</view>
				<view class='action'>
					<view class="cu-avatar-group">
						<view class="cu-avatar round sm" style="background-image:url(https://image.weilanwl.com/img/square-4.jpg);"></view>
						<view class="cu-avatar round sm" style="background-image:url(https://image.weilanwl.com/img/square-3.jpg);"></view>
						<view class="cu-avatar round sm" style="background-image:url(https://image.weilanwl.com/img/square-2.jpg);"></view>
						<view class="cu-avatar round sm" style="background-image:url(https://image.weilanwl.com/img/square-1.jpg);"></view>
					</view>
					<text class='text-grey text-sm'>4 人</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class='content'>
					<text class='icon-btn text-green'></text>
					<text class='text-grey'>按钮</text>
				</view>
				<view class='action'>
					<button class='cu-btn round bg-green shadow'>
						<text class='icon-upload'></text> 上传</button>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class='content'>
					<text class='icon-tagfill text-red'></text>
					<text class='text-grey'>标签</text>
				</view>
				<view class='action'>
					<view class="cu-tag round bg-orange light">音乐</view>
					<view class="cu-tag round bg-olive light">电影</view>
					<view class="cu-tag round bg-blue light">旅行</view>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class='content'>
					<text class='icon-warn text-green'></text>
					<text class='text-grey'>文本</text>
				</view>
				<view class='action'>
					<text class='text-grey text-sm'>小目标还没有实现！</text>
				</view>
			</view>
			<view class="cu-item">
				<view class='content padding-tb-sm'>
					<view>
						<text class='icon-clothesfill text-blue'></text> 多行Item</view>
					<view class='text-gray text-sm'>
						<text class='icon-infofill'></text> 小目标还没有实现！</view>
				</view>
				<view class='action'>
					<switch class='switch-sex sm' @change="switchSex"></switch>
				</view>
			</view>
		</view>

		<view class="cu-bar bg-white solid-bottom margin-top">
			<view class='action'>
				<text class='icon-title text-orange '></text> 消息列表
			</view>
		</view>
		<view class="cu-list menu menu-avatar">
			<view class="cu-item">
				<view class="cu-avatar round lg" style="background-image:url(https://image.weilanwl.com/img/square-1.jpg);"></view>
				<view class='content'>
					<view class='text-grey'>文晓港</view>
					<view class='text-gray text-sm'>
						<text class='icon-infofill text-red'></text> 消息未送达</view>
				</view>
				<view class='action'>
					<view class='text-grey text-xs'>22:20</view>
					<view class="cu-tag round bg-grey sm">5</view>
				</view>
			</view>
			<view class="cu-item">
				<view class="cu-avatar round lg" style="background-image:url(https://image.weilanwl.com/img/square-2.jpg);">
					<view class="cu-tag badge">99+</view>
				</view>
				<view class='content'>
					<view class='text-grey'>文晓港
						<view class="cu-tag round bg-orange sm">SVIP</view>
					</view>
					<view class='text-gray text-sm'>
						<text class='icon-redpacket_fill text-red'></text> 收到红包</view>
				</view>
				<view class='action'>
					<view class='text-grey text-xs'>22:20</view>
					<view class='icon-notice_forbid_fill text-gray'></view>
				</view>
			</view>
			<view class="cu-item ">
				<view class="cu-avatar radius lg" style="background-image:url(https://image.weilanwl.com/img/square-3.jpg);"></view>
				<view class='content'>
					<view>喵星人互动群</view>
					<view class='text-gray text-sm'>
						喵星酱：喵喵喵！</view>
				</view>
				<view class='action'>
					<view class='text-grey text-xs'>22:20</view>
					<view class="cu-tag round bg-red sm">5</view>
				</view>
			</view>
			<view class="cu-item grayscale">
				<view class="cu-avatar radius lg" style="background-image:url(https://image.weilanwl.com/img/square-3.jpg);"></view>
				<view class='content'>
					<view>喵星人互动群</view>
					<view class='text-gray text-sm'>
						喵星酱：喵喵喵！</view>
				</view>
				<view class='action'>
					<view class='text-grey text-xs'>22:20</view>
					<view class="cu-tag round bg-red sm">5</view>
				</view>
			</view>
			<view class="cu-item cur">
				<view class="cu-avatar radius lg" style="background-image:url(https://image.weilanwl.com/img/square-4.jpg);">
					<view class="cu-tag badge"></view>
				</view>
				<view class='content'>
					<view>喵星人互动群
						<view class="cu-tag round bg-orange sm">6人</view>
					</view>
					<view class='text-gray text-sm'>
						喵星酱：
						<text class='icon-picfill text-orange'></text> 图片传输中...</view>
				</view>
				<view class='action'>
					<view class='text-grey text-xs'>22:20</view>
					<view class='icon-notice_forbid_fill text-gray'></view>
				</view>
			</view>
		</view>


		<view class="cu-bar bg-white solid-bottom margin-top">
			<view class='action'>
				<text class='icon-title text-orange '></text> 列表左滑
			</view>
		</view>
		<view class="cu-list menu menu-avatar">
			<view class="cu-item" :class="modalName=='move-box-'+ index?'move-cur':''" v-for="(item,index) in 4" :key='index'
			 @touchstart='ListTouchStart' @touchmove='ListTouchMove' @touchend='ListTouchEnd' :data-target="'move-box-'+index">
				<view class="cu-avatar round lg" :style="'background-image:url(https://image.weilanwl.com/img/square-'+(index+1)+'.jpg);'"></view>
				<view class='content'>
					<view class='text-grey'>文晓港</view>
					<view class='text-gray text-sm'>
						<text class='icon-infofill text-red'></text> 消息未送达</view>
				</view>
				<view class='action'>
					<view class='text-grey text-xs'>22:20</view>
					<view class="cu-tag round bg-grey sm">5</view>
				</view>
				<view class='move'>
					<view class='bg-grey'>置顶</view>
					<view class="bg-red">删除</view>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				num1:0,
				iconList: [{
					icon: 'cardboardfill',
					color: 'red',
					badge: 120,
					name: 'VR'
				}, {
					icon: 'recordfill',
					color: 'orange',
					badge: 1,
					name: '录像'
				}, {
					icon: 'picfill',
					color: 'yellow',
					badge: 0,
					name: '图像'
				}, {
					icon: 'noticefill',
					color: 'olive',
					badge: 22,
					name: '通知'
				}, {
					icon: 'upstagefill',
					color: 'cyan',
					badge: 0,
					name: '排行榜'
				}, {
					icon: 'clothesfill',
					color: 'blue',
					badge: 0,
					name: '皮肤'
				}, {
					icon: 'discoverfill',
					color: 'purple',
					badge: 0,
					name: '发现'
				}, {
					icon: 'questionfill',
					color: 'mauve',
					badge: 0,
					name: '帮助'
				}, {
					icon: 'commandfill',
					color: 'purple',
					badge: 0,
					name: '问答'
				}, {
					icon: 'brandfill',
					color: 'mauve',
					badge: 0,
					name: '版权'
				}],
				gridCol: 3,
				skin: false,
				modalName: '',
				gridBorder: '',
				menuBorder: '',
				menuArrow: '',
				menuCard: '',
				ListTouchStart: '',
				ListTouchDirection: '',

			};
		},
		computed: {
			ngridCol: function() {
				return Number(this.gridCol);
			}
		},
		methods: {
			showModal(e) {
				this.modalName = e.currentTarget.dataset.target;
			},
			hideModal(e) {
				this.modalName = null;
			},
			gridchange: function(e) {
				this.gridCol = e.detail.value;
				console.log(this.gridCol,e.detail.value)
			},
			gridswitch: function(e) {
				this.gridBorder = e.detail.value;
			},
			menuBorders: function(e) {
				this.menuBorder = e.detail.value;
			},
			menuArrows: function(e) {
				this.menuArrow = e.detail.value
			},
			menuCards: function(e) {
				this.menuCard = e.detail.value;
			},
			switchSex: function(e) {
				this.skin = e.detail.value;
			},

			// ListTouch触摸开始
			ListTouchStarts(e) {
				console.log('aaaa');
				this.ListTouchStart = e.touches[0].pageX;
			},

			// ListTouch计算方向
			ListTouchMove(e) {
				this.ListTouchDirection = e.touches[0].pageX - this.ListTouchStart > 0 ? 'right' : 'left';
			},

			// ListTouch计算滚动
			ListTouchEnd(e) {
				if (this.ListTouchDirection == 'left') {
					this.modalName = e.currentTarget.dataset.target;
				} else {
					this.modalName = null;
				}
				this.ListTouchDirection = null;
			}
		}
	}
</script>

<style>
	.page {
		background: #f1f1f1;
	}

	.switch-sex::after {
		content: "\e716";
	}

	.switch-sex::before {
		content: "\e7a9";
	}

	.switch-music::after {
		content: "\e66a";
	}

	.switch-music::before {
		content: "\e6db";
	}
</style>
