<template>
  <div class="sale-board">
    <div class="sale-board-intro">
      <h2>流量分析</h2>
      <p>是指在获得网站访问量基本数据的情况下对有关数据进行统计、分析，从中发现用户访问网站的规律，并将这些规律与网络营销策略等相结合，从而发现目前网络营销活动中可能存在的问题，并为进一步修正或重新制定网络营销策略提供依据。当然这样的定义是站在网络营销管理的角度来考虑的</p>
    </div>
    <div class="sale-board-from">
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          购买数量:
        </div>
        <div class="sale-board-from-line-right">
          <v-counter @on-change="onParamChange('buyNum', $event)" :max = 99 :min = 1></v-counter>
        </div>
      </div>
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          产品类型:
        </div>
        <div class="sale-board-from-line-right">
          <v-selection 
            :selections="buyTypes"
            @on-change="onParamChange('buyType', $event)"
          ></v-selection>
        </div>
      </div>
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          有效时间:
        </div>
        <div class="sale-board-from-line-right">
          <v-chooser 
            :choosers= "periodList"
            @on-change="onParamChange('period', $event)"
          ></v-chooser>
        </div>
      </div>
      <div class="sale-board-from-line">
        <div class="sale-board-from-line-left">
          产品版本:
        </div>
        <div class="sale-board-from-line-right">
           <v-mul-chooser :mulChoose = "versionList" @on-change="onParamChange('versions', $event)"></v-mul-chooser>
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
          <div class="sale-board-from-button" @click="ShowPayDialog">立即购买</div>
        </div>
      </div>
    </div>
    <div class="sale-board-doc">
      <h2>产品说明</h2>
      <p>网站访问统计分析报告的基础数据源于网站流量统计信息，但其价值远高于原始数据资料。专业的网站访问统计分析报告对网络营销的价值，正如专业的财务分析报告对企业经营策略的价值。</p>

      <h3>用户行为指标</h3>
      <ul>
        <li>用户行为指标主要反映用户是如何来到网站的、在网站上停留了多长时间、访问了哪些页面等，主要的统计指标包括：</li>
        <li>用户在网站的停留时间；</li>
        <li>用户来源网站（也叫“引导网站”）；</li>
        <li>用户所使用的搜索引擎及其关键词；</li>
        <li>在不同时段的用户访问量情况等。</li>
      </ul>

      <h3>浏览网站方式</h3>
      <ul>
        <li>用户上网设备类型</li>
        <li>用户浏览器的名称和版本</li>
        <li>访问者电脑分辨率显示模式</li>
        <li>用户所使用的操作系统名称和版本</li>
        <li>用户所在地理区域分布状况等</li>
      </ul>
    </div>
    <bank-dialog :is-show="isShowPayDialog" @on-close="hideShowPayDialog">
      <div class="">
        <table class="buy-dialog-list">
        	<tr>
        	  <th>购买数量</th>
        	  <th>产品类型</th>
        	  <th>有效时间</th>
        	  <th>产品版本</th>
        	</tr>
        	<tr>
        	  <td>{{buyNum}}</td>
        	  <td>{{buyType.label}}</td>
        	  <td>{{period.label}}</td>
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
    <bank-dialog :is-show="isShowErrDialog" @on-close="hideErrDialog">
        支付失败！
    </bank-dialog>
    <check-order :is-show-check-dialog = "isShowCheckOrder" :order-id="orderId" @onCloseCheckDialog="hideCheckOrder"></check-order>
  </div>
</template>

<script>
import vSelection from '../../components/base/selection'
import vChooser from '../../components/base/chooser'
import vCounter from '../../components/base/counter'
import vMulChooser from '../../components/base/mulchooser'
import bankDialog from '../../components/base/dialog'
import bankChooser from '../../components/bankchoose'
import checkOrder from '../../components/checkorder'

export default {
  components: {
    vSelection,
    vChooser,
    vCounter,
    vMulChooser,
    bankDialog,
    bankChooser,
    checkOrder
  },
  data () {
    return {
      buyNum: 1,
      buyType: {},
      versions: [],
      period: {},
      price: 0,
      isShowPayDialog: false,
      isShowCheckOrder: false,
      isShowErrDialog: false,
      orderId: null,
      versionList: [
        {
          label: '客户版',
          value: 0
        },
        {
          label: '代理商版',
          value: 1
        },
        {
          label: '专家版',
          value: 2
        }
      ],
      periodList: [
        {
          label: '半年',
          value: 0
        },
        {
          label: '一年',
          value: 1
        },
        {
          label: '三年',
          value: 2
        }
      ],
      buyTypes: [
        {
          label: '入门版',
          value: 0
        },
        {
          label: '中级版',
          value: 1
        },
        {
          label: '高级版',
          value: 2
        }
      ],
      bankId: null
    }
  },
  methods: {
    onParamChange (attr, val) {
      this[attr] = val
      this.getPrice()
    },
    getPrice () {
      let buyVersionsArray = []
      this.versions.map((item) => {
        buyVersionsArray.push(item.value)
      })
      let reqParams = {
        buyNumber: this.buyNum,
        buyType: this.buyType.value,
        period: this.period.value,
        version: buyVersionsArray.join(',')
      }
      this.$http.get('/api/getPrice', reqParams)
      .then((res) => {
        this.price = res.data.amount
      })
    },
    ShowPayDialog () {
      this.isShowPayDialog = true
    },
    hideShowPayDialog () {
      this.isShowPayDialog = false
    },
    hideCheckOrder () {
      this.isShowCheckOrder = false
    },
    hideErrDialog () {
      this.isShowErrDialog = false
    },
    onChangeBanks (bankObj) {
      this.bankId = bankObj.id
    },
    confirmBuy () {
      let buyVersionsArray = []
      this.versions.map((item) => {
        buyVersionsArray.push(item.value)
      })
      let reqParams = {
        buyNumber: this.buyNum,
        buyType: this.buyType.value,
        period: this.period.value,
        version: buyVersionsArray.join(','),
        bankId: this.bankId
      }
      this.$http.get('/api/createOrder', reqParams)
      .then((res) => {
        this.orderId = res.data.orderId
        this.isShowPayDialog = false
        this.isShowCheckOrder = true
      }, () => {
        this.isShowPayDialog = false
        this.isShowErrDialog = true
      })
    }
  },
  // 在组建渲染完后执行数据重置；
  mounted () {
    this.buyNum = 1
    this.buyType = this.buyTypes[0]
    this.period = this.periodList[0]
    this.version = [this.versionList[0]]
    this.getPrice()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .buy-dialog-list{
    width: 100%;
    text-align: center;
    border-collapse:collapse;
    box-sizing:border-box;
    margin-bottom: 20px;
  }
  .buy-dialog-list th{
    background: rgb(64,172,134);
    border: 1px solid #4fc08d;
    color:#fff;
    padding: 5px 0;
  }
  .buy-dialog-list tr td{
    border:1px solid #E3E3E3;
    padding: 5px 0;
  }
  .buy-dialog-btn{
    background: rgb(64,172,134);
    color: #fff;
    display: inline-block;
    padding: 5px 12px;
  }
</style>
