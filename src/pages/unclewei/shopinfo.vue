<template>
	<section class="chart-container">

		<div class="lee-title1">店铺列表</div>
		<div class="lee-content">
        <!--<div class="editwrap">
            <button class="edit_button"  @click="ModifyiInformation">修改店铺信息</button>
        </div>-->
        <div class="shopwrap">
            <div>
                <label>店铺编号：</label>
            </div>
            <div class="name">
                {{shop_id}}
            </div>
          
        </div>
        <div class="shopwrap">
            <div>
                <label>店铺名称：</label>
            </div>
            <div class="name">
                {{shop.name}}
            </div>
          
        </div>
        <!-- <div class="shopwrap">
            <div>
                <label>主营类目</label>
            </div>
            <div class="name">
                {{shop.shop_type}}
            </div>
           
        </div> -->
        <div class="shopwrap">
            <div>
                <label>创建日期：</label>
            </div>
            <div class="name">
                {{shop.create_time}}
            </div>
        </div>
				<div class="shopwrap">
						<div>
								<label>店铺地址：</label>
						</div>
						<div class="name">
								{{shop.shop_address}}
						</div>
				</div>
				<div class="shopwrap">
						<div>
								<label>店铺定位：</label>
						</div>
						<div class="name">
								经度：<span>{{shop.longitude}}</span> - 纬度：<span>{{shop.latitude}}</span>
						</div>
				</div>
				<div class="shopwrap">
						<div>
								<label>营业时间：</label>
						</div>
						<div class="name">
								{{shop.business_hours}}
						</div>
				</div>
				<div class="shopwrap">
						<div>
								<label>客服电话：</label>
						</div>
						<div class="name">
								{{shop.cs_phone}}
						</div>
				</div>
				<div class="shopwrap">
						<div>
								<label>店铺地wifi：</label>
						</div>
						<div class="name">
								wifi 名称：<span>{{shop.shop_wifi_name}}</span> - wifi 密码：<span>{{shop.shop_wifi_pwd}}</span>
						</div>
				</div>
        <div class="shopwrap">
						<div>
								<label>是否显示店铺信息：</label>
						</div>
						<div class="name">
								{{shop.shop_info_isshow=='1'?'是':'否'}}
						</div>
				</div>
        <div class="shopwrap">
						<div>
								<label>是否显示优惠券：</label>
						</div>
						<div class="name">
								{{shop.is_cash=='1'?'是':'否'}}
						</div>
				</div>
        <div class="shopwrap shopwrap2" v-if="shop.is_cash=='1'">
						<div>
								<label>优惠券缩略图：</label>
						</div>
						<div class="thumbnail">
                <img :src="shop.cash_bg_img">
						</div>
				</div>
        <div class="shopwrap">
						<div>
								<label>首页是否显示团购：</label>
						</div>
						<div class="name">
								{{shop.is_group=='1'?'是':'否'}}
						</div>
				</div>
        <div class="shopwrap shopwrap2" v-if="shop.is_group=='1'">
						<div>
								<label>团购缩略图：</label>
						</div>
						<div class="thumbnail">
								<img :src="shop.group_bg_img">
						</div>
				</div>
        <div class="shopwrap">
						<div>
								<label>首页是否显示砍价：</label>
						</div>
						<div class="name">
								{{shop.is_bargain=='1'?'是':'否'}}
						</div>
				</div>
        <div class="shopwrap shopwrap2" v-if="shop.is_bargain=='1'">
						<div>
								<label>砍价缩略图：</label>
						</div>
            <div class="thumbnail">
                <img :src="shop.bargain_bg_img">
            </div>
				</div>
        <div class="shoplogo">
            <div>
                <label>店铺logo：</label>
            </div>
            <div class="logo">
                <img :src="shop.logo">
            </div>
        </div>
        <div class="bgwrap">
            <div>
                <label>店铺背景图</label>
            </div>
            <div class="bg">
                <div class="bg_imags" v-for="(item,index) of shop.bg_picture_url" :key="index">
                  <img :src="item" class="imags_list">
                </div>
            </div>
        </div>
				
        <!-- <div class="infowrap">
            <div>
                <label>店铺简介</label>
            </div>
            <textarea>{{shop.member_info}}</textarea>
        </div> -->
        <div class="money">
            <div>
              <label>店铺余额：</label>
            </div>
            <div class="money_num">
              ￥{{moneynum}}
            </div>
            <a class="get_money" href="https://pay.weixin.qq.com/index.php/core/home/login?return_url=%2F" target="_blank">查看</a> 
        </div>
       <!-- 余额提现 -->
      <!--  <el-dialog title="余额提现" :visible.sync="showmoney" class="get_money_dialog">
          <el-form :model="money_form" label-width="100px">
            <el-form-item label="可提现余额" class='get_money_num'>￥{{moneynum}}</el-form-item>
            <el-form-item label="提现金额">
              <el-input class="moneyinput" placeholder="请输入提现金额，最低1元" v-model="money_form.money"></el-input>
            </el-form-item>
            <el-form-item label="支付宝">
              <el-input placeholder="暂只支持支付宝提现，请输入支付宝账号" v-model="money_form.phone"></el-input>
            </el-form-item>
            <el-form-item label="真实姓名">
              <el-input placeholder="请输入您的姓名以便验证账户" v-model="money_form.realname"></el-input>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer">
            <button @click="showmoney = false" class="cancle">取 消</button>
            <button class="get_money_comfirm" @click="money_comfirm">确认</button>
          </div>
       </el-dialog> -->
       <!-- 提现成功 -->
       <!-- <el-dialog title="提现成功" :visible.sync="show_success" class="get_money_success">
          <div class="success_message">￥{{this.money_form.money}} 已提现成功，将在三个工作日内转至您的支付宝账户！有任何问题请随时联系客服！</div>
       </el-dialog> -->
       <!-- 修改信息 -->
      <!--  <el-dialog title="修改信息" :visible.sync="edit_shopinfo">
          <el-form :model="shop">
            <el-form-item label="店铺名称" :label-width="formLabelWidth">
              <el-input v-model="shop.name" auto-complete="off"></el-input>
            </el-form-item>
            <el-form-item label="上传店铺logo" :label-width="formLabelWidth">
          <el-upload
        class="avatar-uploader"
        action="https://www.huixianfeng.net/upload_img"
        :show-file-list="true"
        :on-success="handleAvatarSuccess"
        :before-upload="beforeAvatarUpload">
        <img v-if="imageUrl" :src="imageUrl" class="avatar">
        <i v-else class="el-icon-plus avatar-uploader-icon"></i>
      </el-upload>
        </el-form-item>
            <el-form-item label="上传背景图片" :label-width="formLabelWidth">
              <el-upload
              class="upload-demo"
              drag
              action="https://www.huixianfeng.net/upload_img"
              :on-success='uploadsuccess'
              :before-upload="beforeDemoUpload"
              multiple>
              <img v-if="backimageUrl" :src="backimageUrl" class="backimage">
              <i v-else class="el-icon-upload"></i>
              <div  class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
              <div class="el-upload__tip" slot="tip">只能上传jpg/png文件，且不超过2M</div>
            </el-upload>
            </el-form-item>
          </el-form>
          <div class="options">
                <button class="cancle_edit" @click="dialogFormVisible = false">取消</button>
                <button class="comfirm" @click="nextStep">下一步</button>
          </div>
        </el-dialog> -->

       <!--  <el-dialog title="" :visible.sync="secondStep">

          <el-form :model="shop"> -->
<!--             <el-form-item label="输入会员须知：" :label-width="formLabelWidth">
              <el-input
                  type="textarea"
                  :autosize="{ minRows: 4, maxRows: 10}"
                  placeholder="请输入内容"
                  v-model="shop.member_info">
                </el-input>
            </el-form-item> -->
            
       <!-- <el-form-item label="请选择行业类型" :label-width="formLabelWidth">
          <el-radio-group v-model="shop.shoptype" class="type_choose">
            <el-radio label="食品" class="type-one"></el-radio>
            <el-radio label="服装"></el-radio>
            <el-radio label="数码家电"></el-radio>
            <el-radio label="日用百货"></el-radio>
            <el-radio label="美妆"></el-radio>
            <el-radio label="医疗健康"></el-radio>
            <el-radio label="虚拟内容"></el-radio>
            <el-radio label="其他"></el-radio>
          </el-radio-group>
        </el-form-item>
          </el-form>
          <div class="options">
                <button class="cancle_edit" @click="secondStep = false">取消</button>
                <button class="comfirm" @click="update_shop">完成</button>
          </div>
        </el-dialog> -->

        </div>
    </section>
</template>
<script type="text/javascript">
import * as store from '@/utils/sdk/store'
import {update_shop,shop_desc,downfile,money,deposit,admin_shop_info} from '@/utils/api'
import '@/utils/jquery'

export default{
    data(){
        return{
          shop:{},
          shopqrcode:'',
          moneynum:'',
          edit_shopinfo: false,
          secondStep: false,
          showmoney:false,
          show_success:false,
          money_form:{
            phone:'',
            realname:'',
            money:''
          },
          shop_id:store.get('currentshopid'),
          shop: {
                    member_type: true,
                    member_money: '',
                    name: '',
                    photo: '',
                    plan_code: '',
                    member_info: '',
                    shoptype:'',
                    shop_info_isshow:'',
                    is_group:'',
                    group_bg_img:'',
                    is_bargain:'',
                    bargain_bg_img:'',
                    is_cash:'',
                    cash_bg_img:'',
                    bg_picture_url:[]
          },
          formLabelWidth: '180px',
          imageUrl: '',
          backimageUrl:''
        }
            },
        
    methods:{
			ModifyiInformation(){
				this.$router.push({path:'/business/shop/modify'})
			},
        money_comfirm(){
            var flag=true
            if (this.money_form.money=='') {
                this.$message.error('请输入提现金额')
            }
            else if (eval(this.moneynum)<eval(this.money_form.money)){
              this.$message.error('提现金额必须小于账户余额')
            }
            else if (this.money_form.realname=='') {
              this.$message.error('请输入您的姓名，方便进行账户验证')
            }
            else if (this.money_form.phone=='') {
              this.$message.error('请输入您的支付宝账号')
            }else {
              flag=false
            }
            if (flag==false) {
              deposit({
                phone:this.money_form.phone,
                realname:this.money_form.realname,
                money:this.money_form.money
              }).then((res)=>{
                if (res.error_code==1000) {
                  this.showmoney=false
                  this.money()
                  this.show_success=true
                }else if (res.error_code==1002) {
                  this.$message.error(res.msg)
                };
                
              })
            };
            
        },
        shop_desc(){
            const downloadUrl = 'https://www.huixianfeng.net/downfile?filename='
            admin_shop_info({shop_id:store.get('currentshopid')}).then((res)=>{
              if (res.error_code==1000) {
                console.log(res.data,'00000')
                this.shopqrcode = downloadUrl + res.data.qrcode
                this.shop=res.data
                if(res.data.bg_picture_url!=null){
                    this.shop.bg_picture_url=res.data.bg_picture_url.split(",")
                }else{
                    this.shop.bg_picture_url=[]
                }
                
                console.log(this.shop.bg_picture_url)
              };

            })
        },
        money(){
          money({shop_id:store.get('currentshopid')}).then((res)=>{
            if (res.error_code==1002) {
                    this.$message.error('res.msg')
                  };
                  if (res.error_code==1000) {
                    this.moneynum = res.data
                  };
          })
        },
        nextStep () {
          this.edit_shopinfo = false
          sleep(300)
          this.secondStep = true
        },
        update_shop(){
            let params = {
                member_type: this.shop.member_type,
                member_money: this.shop.member_money,
                name: this.shop.name,
                logo:this.shop.logo,
                photo: this.shop.photo,
                member_info: this.shop.member_info,
                shop_type:this.shop.shoptype,
                shop_id:store.get('currentshopid')
            }
            params.token = store.get('token')
            update_shop({params}).then((res)=>{
              if (res.error_code==1000) {
                this.secondStep=false
                this.$message.success('修改成功')
                this.shop_desc()
              };
            })
        },
         uploadsuccess (response, file, fileList) {
             this.shop.photo = response.data.img_url
           },
            beforeAvatarUpload(file){
      const isJPG = file.type === 'image/jpeg'||'image/png'||'image/bmp'||'image/jpg'
      const isLt2M = file.size / 1024 / 1024 < 2

      if (!isJPG) {
        this.$message.error('上传头像图片只能是 JPG/PNG/BMP 格式!')
      }
      if (!isLt2M) {
        this.$message.error('上传头像图片大小不能超过 2MB!')
      }
      return isJPG && isLt2M
    },
    beforeDemoUpload (file) {
      const isJPG = file.type === 'image/jpeg'||'iamge/png'||'image/bmp'||'image/jpg'
      const isLt2M = file.size / 1024 / 1024 < 2

      if (!isJPG) {
        this.$message.error('上传头像图片只能是 JPG/PNG/BMP 格式!')
      }
      if (!isLt2M) {
        this.$message.error('上传头像图片大小不能超过 2MB!')
      }
      return isJPG && isLt2M
    },
    handleAvatarSuccess(res,file){
      this.imageUrl = URL.createObjectURL(file.raw)
      console.log(res,'0009090')
      this.shop.logo = res.data.img_url
    },
    },
    created(){
        this.shop_desc()
        this.money()
    },
    
    
}
function sleep(numberMillis) {  
    var now = new Date();  
    var exitTime = now.getTime() + numberMillis;  
    while (true) {  
        now = new Date();  
        if (now.getTime() > exitTime)  
        return;  
        }  
}
</script>

<style lang="stylus" scoped>
.thumbnail img
  width 120px
  height 64px
.type_choose
  margin-left 20px
  display flex
  flex-wrap wrap
  justify-content space-between
.el-radio+.el-radio
  margin-left 0
.el-radio
  width 50%
  margin-left 0
.chart-container
    margin-top 30px
    position relative
.editwrap
    position absolute
    top 0
    right 80px
.el-button
    border none
    background-color white
    padding 8px 10px
.el-button--primary
    color #409eff
.el-button:hover
    color #ff6c34
textarea
    width 300px
    height 100px
    background-color #f9f9f9
    border-radius 6px
    margin-top 10px
    padding 10px 20px
    font-size 15px
label
    display block
    width 150px
    font-weight 400
    margin-left 60px
    color #323232
    height 40px
    line-height 40px
    font-size 15px
.shopwrap2
    margin:25px 0 55px
.shopwrap
    height 40px
    line-height 40px
    display flex
    .name 
        font-size 15px
        line-height 40px
        color #323232
.qrcodewrap
    height 60px
    display flex
    .qrcode
      display flex
      img
        height 50px
        width 50px
    .downfile
        color #0089e1
        cursor pointer
        line-height 50px
        margin-left 30px
    
.shoplogo
    margin-top 60px
    height 60px
    display flex
    .logo 
        display flex
        img
           border-radius 50%
           height 50px
           width 50px
           z-index 0
 
.bgwrap
    margin-top 10px
    margin-bottom 160px
    height 120px
    display flex
    .bg
        margin-top 10px
        img
            height 64px
            width 120px
            margin-right 5px
.typewrap
    height 60px
    line-height 60px
    display flex
    
.infowrap
    line-height 40px
    margin-top 20px
    display flex
.money
    display flex
    margin-top 140px
    background-color #B6D4E8
    font-size 15px
    .money_num
      color #ff6c34
      line-height 40px
      font-size 20px
    .get_money
      margin-left 20px
      line-height 40px
      font-size 15px
      cursor pointer
      color #409eff
.el-form-item
    margin-bottom 20px
.get_money_dialog
    width 70%
    left 15% 
.get_money_num
    color #ff6c34
    margin-bottom 8px
.el-input
    width 80%
    .el-input__inner
      padding none
.dialog-footer
    display flex 
    justify-content space-between
    padding 0 90px
    margin-top 27px
.cancle
  color #c0c4cc
  border 1px solid #c0c4cc
  cursor pointer
  padding 5px 20px
  border-radius 3px
  background-color white
.get_money_comfirm
  color white
  background-color #409EFF
  cursor pointer
  padding 5px 20px
  border-radius 3px
.get_money_success
  width 60%
  margin-left 20%
.success_message
  padding 0 20px 30px

.avatar-uploader .el-upload {
    border: 1px dashed black;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
.avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
.avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 80px;
    height: 80px;
    line-height: 80px;
    text-align: center;
  }
.avatar {
  width 60px
  height 60px
  }
.el-icon-upload{
    margin 20px 0 0
  }
.edit_button
  padding 2px 10px
  border 1px solid #409EFF
  background-color #f9f9f9
  border-radius 5px
  color #409EFF
  cursor pointer

.options
    margin-top 20px
    display flex 
    justify-content space-between
    padding 0 15%
.cancle_edit
  color #C0C4CC
  background-color white
  cursor pointer
  padding 5px 20px 
  border-radius 3px
  border 1px solid #C0C4CC
.comfirm
  color white
  background-color #409EFF
  cursor pointer
  padding 5px 20px
  border-radius 3px
  border 1px solid #409EFF
.el-checkbox-group
  display flex
  flex-wrap wrap
  width 88%
</style>
<style lang="stylus" scoped>
	.shoplogo .logo img{
		width: auto;
		max-width: 100px;
	}
	
	.shoplogo{
		height: auto;
		}
	.bg_imags{
    display:inline-block;
  }
	@media(max-width:900px) {
  .bg_imags{
    display:block;
  }
  .bg .bg_imags .imags_list{
      width:180px;
  }
	.chart-container{
		margin-top: 0;
	}
	.lee-content{
		background: #FFFFFF;
		font-size: 14px;
		color: #555555; 
		padding-top: 20px;
		}
	label{
		margin-left:15px;
		width:auto;
	}
	label,
	.shopwrap .name{
		color: #555555;
		font-size: 14px;
	}
    
	.shoplogo .logo{
			margin-top: 0;
		}
	.shoplogo label{
		line-height: 50px;
		height: 50px;
	}
	.money{
		font-size: 16px;
		margin-top: 50px;
	}
	.div .body .el-main .content-wrapper{
		padding-bottom: 0;
	}

	}
</style>
