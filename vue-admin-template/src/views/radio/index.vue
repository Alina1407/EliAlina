<template>
	<div id="content">
		<div class="banner">
			<p>时夕乐听网
				<br>获取无限的音频
				<br>学习快乐
			</p>
			<div>
				<a class="btnStar" href="#">立即开始</a>
				<a class="btnLogin">注册</a>
			</div>
		</div>
		<div class="conBottom" :class="{'active':isActive}">
			<div class="conLeft">
				<div>
					<p>
						<span class="srcFa" :class="{'active':isActive}">{{addFa}} <i>&gt;</i> {{addSon}}</span>
						<span class="navStop" @click="isActive=false">收起</span>
					</p>
					<ul>
						<li v-for="item in radioData" :key="item.id"
							:class="{'active':item.name == focusLi ? true : false}" @click="navOne(item)">
							{{item.name}}<span v-if="item.isNew">新</span></li>
					</ul>
					<ul class="navTwo" :class="{'active':isActive}">
						<li v-for="(item,index) in navTwoCon" :key="index"
							:class="{'active1':item.name == focusLi2 ? true : false}" @click="navTwo(item)">
							{{item.name}}
						</li>
					</ul>
				</div>
			</div>
			<div class="conRight">
				<el-table
						:data="sonList"
						style="width: 100%">
					<el-table-column
							label="操作"
							width="100">
						<template slot-scope="scope">
							<div class="img"><img :src="scope.row.image" alt=""></div>
						</template>
					</el-table-column>
					<el-table-column
							prop="name"
							label="姓名"
							width="180">
					</el-table-column>
					<el-table-column
							prop="address"
							label="地址">
					</el-table-column>
				</el-table>
				<!--				<ul :class="{'active':isActive}">-->
				<!--					<li v-for="(item,index) in sonList" :key="index">-->
				<!--						<div class="img"><img :src="item.image" alt=""></div>-->
				<!--						<div class="icon">{{item.icon}}</div>-->
				<!--						<div class="name">{{item.name}}</div>-->
				<!--						<div class="titbox"><span>{{item.name}}</span><span>{{item.tit}}</span></div>-->
				<!--						<div class="num">{{item.num}}集</div>-->
				<!--					</li>-->
				<!--				</ul>-->
			</div>
		</div>
	</div>
</template>

<script>
	// import { getList } from '@/api/table'
	import radioData from './data.js'

	export default {
		data() {
			return {
				radioData: [],
				isActive: false,
				navTwoCon: [],
				sonList: [],
				focusLi: '',
				addFa: '',
				addSon: '',
				focusLi2: ''
			}
		},
		created() {
			this.radioData = radioData.nav;
			this.sonList = radioData.content;
		},
		methods: {
			/*点击一级菜单事件*/
			navOne(obj) {
				this.isActive = true;
				this.navTwoCon = obj.childen;
				this.focusLi = obj.name;
				this.addFa = obj.name;
				// console.log(this.addFa,"obj")
			},
			navTwo(obj) {
				this.addSon = obj.name;
				this.focusLi2 = obj.name;
				// console.log(this.addSon,"obj")
			}
		}
	}
</script>

<style lang="scss">
	@import "~@/styles/mixin.scss";
	@import "~@/styles/variables.scss";
	
	#content {
		background: #171717;
		min-height: 100%;
		
		.banner {
			width: 100%;
			height: 26.875rem;
			background-image: url(../../img/bannerbg.png);
			padding: 75px 135px;
			
			p {
				font-size: 64px;
				font-weight: bold;
				color: #FFFFFF;
			}
			
			div {
				a {
					display: inline-block;
					border-radius: 10px;
					font-weight: bold;
					font-size: 14px;
					margin-top: 28px;
					
					&.btnStar {
						padding: 19px 52px;
						background: #ffda2a;
						
						&:hover {
							padding: 16px 52px;
							transition: all 0.3s;
						}
					}
					
					&.btnLogin {
						border: 2px solid #ffda2a;
						padding: 17px 30px;
						margin-left: 15px;
						color: #ffda2a;
						
						&:hover {
							background: #ffda2a;
							color: #000;
							transition: all 0.3s;
							padding: 15px 30px;
						}
					}
				}
			}
		}
		
		.conBottom {
			background: #171717;
			padding-bottom: 54px;
			width: 100%;
			display: inline-block;
			position: relative;
			min-height: 600px;
			
			&.active {
				.conRight {
					width: calc(100% - 380px);
					margin-left: 380px;
				}
				
				.conLeft {
					width: 380px;
				}
			}
			
			.conLeft {
				// transition: all 0.35s;
				width: 260px;
				padding-top: 32px;
				display: inline-block;
				position: absolute;
				left: 0;
				
				div {
					position: relative;
					padding-left: 60px;
					
					p {
						color: #7e7e7e;
						font-size: 12px;
						position: relative;
						
						.srcFa {
							position: absolute;
							left: 20px;
							opacity: 0;
							transition: all 0.35s;
							
							&.active {
								left: 40px;
								opacity: 1;
							}
						}
						
						.srcSon {
							position: absolute;
							left: 90px;
						}
					}
					
					ul {
						float: left;
						list-style: none;
						width: 170px;
						padding: 0;
						
						li {
							color: #bdbdbd;
							font-size: 14px;
							margin-top: 40px;
							cursor: pointer;
							position: relative;
							
							&.active {
								color: #ffda2a;
							}
							
							&:hover {
								color: #FFFFFF;
								transition: all 0.35s;
								font-weight: bold;
							}
							
							span {
								font-size: 12px;
								color: #ffda2a;
								position: absolute;
								top: -4px;
							}
							
						}
					}
					
					.navTwo {
						width: 150px;
						height: 270px;
						opacity: 0;
						left: 170px;
						overflow-y: scroll;
						position: absolute;
						transition: all 0.35s;
						
						&.active {
							left: 230px;
							opacity: 1;
						}
						
						li {
							&.active1 {
								color: #ffda2a;
							}
							
						}
						
						
					}
				}
			}
			
			.conRight {
				width: calc(100% - 270px);
				display: inline-block;
				padding-right: 60px;
				margin-left: 270px;
				transition: all 0.35s;
				color: #FFFFFF;
				
				.colorWhite {
					color: #ffffff;
				}
				
				.colorGary {
					color: #717273;
				}
				
				.el-table th {
					display: none;
				}
				
				.el-table th, .el-table tr {
					background: #171717;
				}
				
				.el-table td {
					border-bottom: 1px solid #2C2D2E;
					font-size: 12px;
				}
				
				.el-table::before {
					height: 0px;
				}
				
				.el-table--enable-row-hover .el-table__body tr:hover > td {
					background: #000;
				}
				
				.img {
					width: 96px;
					height: 42px;
					overflow: hidden;
					
					img {
						width: 100%;
					}
				}
				
				ul {
					width: 100%;
					padding: 0;
					
					li {
						list-style: none;
						width: 100%;
						height: 90px;
						float: left;
						border-top: 1px solid #2d2d2d;
						transition: all 0.35s;
						
						&:hover {
							background: #0e0e0e;
						}
						
						.img {
							width: 96px;
						}
					}
					
				}
				
			}
		}
	}
</style>
