<template>
  <div class="sale-board">
    <div class="sale-board-intro">
      <h2>广告发布</h2>
      <p>广告活动按照广告计划执行，到完成广告创作并形成广告作品之后，经过广告主的最后审核同意，即可送到预定的媒介发布刊播。这项工作一般由媒介部门的有关专业人员负责，他们的任务就是专门负责与有关媒介单位接洽，安排有关广告的发播事宜，并对发播质量实施监督。</p>
    </div>
    <div class="sale-board-from">
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          购买数量:
        </div>
        <div class="sale-board-from-line-right">
          <v-counter @on-change="onParamChange('buyNum', $event)"></v-counter>
        </div>
      </div>
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          产品类型:
        </div>
        <div class="sale-board-from-line-right">
          <v-selection :selections="versionList" @on-change="onParamChange('buyType', $event)"></v-selection>
        </div>
      </div>
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          有效时间:
        </div>
        <div class="sale-board-from-line-right">
          半年
        </div>
      </div>
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          产品版本:
        </div>
        <div class="sale-board-from-line-right">
           <v-mul-chooser :mulChoose = "tradeList" @on-change="onParamChange('versions', $event)"></v-mul-chooser>
        </div>
      </div>
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          总价:
        </div>
        <div class="sale-board-from-line-right">
         {{price * buyNum}}元
        </div>
      </div>
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          &nbsp;</div>
        <div class="sale-board-from-line-right">
          <div class="sale-board-from-button" @click="showPayDialog">立即购买</div>
        </div>
      </div>
    </div>
    <div class="sale-board-doc">
      <h2>产品说明</h2>
      <p>广告活动按照广告计划执行，到完成广告创作并形成广告作品之后，经过广告主的最后审核同意，即可送到预定的媒介发布刊播。这项工作一般由媒介部门的有关专业人员负责，他们的任务就是专门负责与有关媒介单位接洽，安排有关广告的发播事宜，并对发播质量实施监督。</p>
      <table class="sales-board-table">
          <tbody>
              <tr class="ui-table-row">
                  <td class="col-first">
                      <div class="intro-pic">
                          <label>安全安保</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>办公文教</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>彩票</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>车辆物流</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>成人用品</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>出版传媒</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>电脑硬件</label>
                      </div>
                  </td>
              </tr>
              <tr class="ui-table-row">
                  <td class="col-first">
                      <div class="intro-pic">
                          <label>电子电工</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>房地产建筑装修</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>分类平台</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>服装鞋帽</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>箱包饰品</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>化工原料制品</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>机械设备</label>
                      </div>
                  </td>
              </tr>
              <tr class="ui-table-row">
                  <td class="col-first">
                      <div class="intro-pic">
                          <label>家庭日用品</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>家用电器</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>教育培训</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>节能环保</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>金融服务</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>礼品</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>旅游住宿</label>
                      </div>
                  </td>
              </tr>
              <tr class="ui-table-row">
                  <td class="col-first">
                      <div class="intro-pic">
                          <label>美容化妆</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>母婴护理</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>农林牧渔</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>软件</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>商务服务</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>生活服务</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>食品保健品</label>
                      </div>
                  </td>
              </tr>
              <tr class="ui-table-row">
                  <td class="col-first">
                      <div class="intro-pic">
                          <label>手机数码</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>通讯服务设备</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>网络服务</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>医疗服务</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>游戏</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>运动休闲娱乐</label>
                      </div>
                  </td>
                  <td>
                      <div class="intro-pic">
                          <label>招商加盟</label>
                      </div>
                  </td>
              </tr>
          </tbody>
      </table>
    </div>
    <bank-dialog :is-show="isShowPayDialog">
       <div class="">
        <table class="buy-dialog-list">
          <tr>
            <th>购买数量</th>
            <th>产品类型</th>
            <th>产品版本</th>
          </tr>
          <tr>
            <td>{{buyNum}}</td>
            <td>{{buyType.label}}</td>
            <td>
              <span v-for="item in versions">{{ item.label }}； </span>
            </td>
          </tr>
        </table>
        <h2>请选择银行</h2>
        <bank-chooser @on-change="onChangeBanks"></bank-chooser>
        <div class="buy-dialog-btn" @click="confirmBuy">确认购买</div>
      </div>
    </bank-dialog>
    <bank-dialog :is-show="isShowErrDialog">
    支付失败！</bank-dialog>
    <check-order :is-show-check-dialog="isShowCheckDialog" @on-close-check-dialog = "hideCheckDialog"></check-order>
  </div>
</template>

<script>
import vSelection from '../../components/base/selection'
import vMulChooser from '../../components/base/mulchooser'
import vCounter from '../../components/base/counter'
import checkOrder from '../../components/checkorder'
import bankChooser from '../../components/bankchoose'
import bankDialog from '../../components/base/dialog'

export default {
  components: {
    vSelection,
    vMulChooser,
    vCounter,
    bankChooser,
    bankDialog,
    checkOrder
  },
  data () {
    return {
      isShowErrDialog: false,
      isShowCheckDialog: false,
      isShowPayDialog: false,
      buyNum: 1,
      buyType: {},
      versions: [],
      price: 0,
      bankId: null,
      tradeList: [
        {
          label: '出版业',
          value: 0
        },
        {
          label: '媒体',
          value: 1
        },
        {
          label: '金融',
          value: 2
        },
        {
          label: '互联网',
          value: 3
        },
        {
          label: '游戏',
          value: 4
        }
      ],
      versionList: [
        {
          label: '初级版',
          value: 0
        },
        {
          label: '中级版',
          value: 1
        },
        {
          label: '高级版',
          value: 2
        },
        {
          label: '专家版',
          value: 3
        }
      ]
    }
  },
  methods: {
    onParamChange (attr, val) {
      this[attr] = val
      this.getPrice()
    },
    getPrice () {
      let nowVersionArray = []
      this.versions.map((item) => {
        nowVersionArray.push(this.versions)
      })
      let regParam = {
        buyNumber: this.buyNum,
        buyTpye: this.buyType,
        version: nowVersionArray.join(',')
      }
      this.$http.get('/api/getPrice', regParam)
      .then((res) => {
        this.price = res.data.amount
      })
    },
    showPayDialog () {
      this.isShowPayDialog = true
    },
    showErrDialog () {
      this.isShowErrDialog = true
    },
    hideCheckDialog () {
      this.isShowCheckDialog = false
    },
    onChangeBanks (bank) {
      this.bankId = bank.id
    },
    confirmBuy () {
      let nowArray = []
      this.versions.map((item) => {
        nowArray.push(item.label)
      })
      let reqParam = {
        buyNum: this.buyNum,
        buyType: this.buyType.value,
        version: nowArray.join(','),
        bankId: this.bankId
      }
      this.$http.get('/api/createOrder', reqParam)
      .then(() => {
        this.isShowPayDialog = false
        this.isShowCheckDialog = true
      }, _ => {
        this.isShowPayDialog = false
        this.isShowErrDialog = true
      })
    }
  },
  mounted () {
    this.buyNum = 1
    this.buyType = this.tradeList[0]
    this.versions = [this.versionList[0]]
    this.getPrice()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
