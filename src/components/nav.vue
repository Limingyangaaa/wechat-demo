<template>
  <section class="nav_box">
    <div class="nav_title">
      <div class="nav_title_text" v-for="(item, index) in navList" @click.prevent="textEvent(index, item)" :class="{underline: index==current}">
        <div class="child_main">
          <span class="child_text">{{item.title}}</span>
          <span class="select_btn" v-if="item.child" @click.prevent.stop="btnEvent()"></span>
        </div>
        <div class="child_box" v-if="item.child && childFlag">
          <div class="title_child" v-for="(item1, index1) in item.child" @click="childSelectEvent($event, item1, item1.index)">{{item1.title}}</div>
        </div>
      </div>
    </div>
    <div class="contentMain">
      <div class="listCount" v-for="(item, num) in dataMenu">
        <div class="listItem">
          <div class="listTitle">
            <span class="titleLogo">{{item.clientStatus}}</span>
          </div>
          <div class="listMain">
            <div class="mainItem">
              <div class="itemType">报案人</div>
              <div class="itemDetail">{{item.reportName}}</div>
            </div>
            <div class="mainItem">
              <div class="itemType">车牌号</div>
              <div class="itemDetail">{{item.carMark}}</div>
            </div>
            <div class="mainItem">
              <div class="itemType">是否大案</div>
              <div class="itemDetail">{{item.majorCase}}</div>
            </div>
            <div class="mainItem">
              <div class="itemType">出险时间</div>
              <div class="itemDetail">{{item.accidentTime}}</div>
            </div>
            <div class="mainItem">
              <div class="itemType">出险地点</div>
              <div class="itemDetail">{{item.accidentSite}}</div>
            </div>
            <div class="mainItem">
              <div class="itemType">推修网点</div>
              <div class="itemDetail">{{item.garageName}}</div>
            </div>
            <div class="mainTel"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
    props: {
       webCurrentIndex: {
         type: String,
         default: '111'
       }
    },
  data () {
    return {
      select: 0,
      webNum: '111',
      selectNum: '01',
      selectChildNum: '01',
      submitNum: '01',
      childFlag: false,
      current: 0,
      navList: [
        {
          title: '全部',
          index: '01',
          child: [
            {title: '全部', index: '01'},
            {title: '确认到店', index: '03'},
            {title: '拒绝到店', index: '04'}
          ]
        },
        {title: '确认到店', index: '03'},
        {title: '拒绝到店', index: '04'}
      ],
      dataMenu: [{
          clientStatus: '确认到店',
          reportName: '北***',
          carMark: '******',
          majorCase: 'N',
          accidentTime: '2015-01-16 17:04:00',
          accidentSite: '北京市-海淀区-厂桂中路',
          garageName: '聊城新世纪汽车销售有限公司'
        }
      ],
      arr: [
        [
          {
            clientStatus: '确认到店',
            reportName: '北***',
            carMark: '******',
            majorCase: 'N',
            accidentTime: '2015-01-16 17:04:00',
            accidentSite: '北京市-海淀区-厂桂中路',
            garageName: '聊城新世纪汽车销售有限公司'
          }
        ]
      ,
      [
        {
            clientStatus: '确认到店',
            reportName: 'P***',
            carMark: '******',
            majorCase: 'N',
            accidentTime: '2016-05-24 17:04:00',
            accidentSite: '广东省-广州市-番禺区-东兴小学',
            garageName: '北京热龙汽车服务有限公司'
          },
          {
            clientStatus: '确认到店',
            reportName: '深***',
            carMark: '******',
            majorCase: 'N',
            accidentTime: '2017-02-16 17:04:00',
            accidentSite: '山东省-泰安市-泰山区-灵山大街-岭山庄',
            garageName: '聊城新世纪汽车销售有限公司'
          }
      ]
      ]
    }
  },
  methods: {
    textEvent (index, item) {
      this.current = index
    },
    childSelectEvent (e, item, index) {
      this.navList[0].title=item.title;
      this.selectChildNum = index
      this.submitNum = index
      // e.target.parentElement.parentElement.querySelector('.child_text').innerText = item.title
      this.childFlag = !this.childFlag
    },
    btnEvent () {
      this.childFlag = !this.childFlag
    },
    changeContent (index, num, web, ee) {
      console.log('index:', index, '网点编号:', web, ee)
      if (this.select == 0) {
        this.select = 1
        this.dataMenu = this.arr[1]
      } else {
        this.select = 0
        this.dataMenu = this.arr[0]
      }
    },
    transformEvent () {
       if (this.childFlag == true) {
         this.childFlag = !this.childFlag
      }
    }
  },
  watch: {
    current (cur, old) {
      switch (cur) {
        case 0: this.selectNum = '01'
                  break;
        case 1: this.selectNum = '03'
                  break;
        case 2: this.selectNum = '04'
                  break;
        default: break;
      }
      this.submitNum = this.selectNum
      this.changeContent(this.selectNum, this.webNum, this.webCurrentIndex, 'current has changed')
    },
    selectChildNum (cur, old) {
      this.submitNum = this.selectNum
        this.changeContent(this.selectChildNum, this.webNum, this.webCurrentIndex, 'selectChildNum has changed')
    },
    webCurrentIndex (cur, old) {
       this.changeContent(this.submitNum, this.webNum, this.webCurrentIndex, 'webCurrentIndex has changed')
    }
  }
}
</script>

<style>
  .nav_title {
    height :80rpx;
    display: flex; 
    flex-direction: row;
    justify-content: center;
    align-items: center;
    border-bottom: #eee;
    font-size: 30rpx;
  }
  .nav_title_text {
    font-size: 30rpx;
    width:33%;
    height: 100%;
    display: flex;
    flex-direction :column;
    justify-content: center;
    align-items: center;
    position: relative;
  }
  .child_main {
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  .select_btn {
    position:absolute;
    right: 24rpx;
    height: 30rpx;
    width: 30rpx;
    border-radius: 15rpx;
    background: #ccc;
  }
  .child_box {
    position: absolute;
    top: 0;
    width:100%;
    border:1px solid #ccc;
    left:0;
    z-index:99999;
    font-size: 30rpx;
    background: #fff;
  }
  .title_child {
    height: 1rem;
    display: flex;
    justify-content: center;
  align-items: center;
  }
  .underline {
    border-bottom: 1px solid orange;
  }
  .contentMain{
    position: fixed;
    width: 100%;
    height: calc(100% - 2rem);
    overflow-y: scroll;
  }
  .listItem {
    background: #fff;
  }
  .listMain {
    margin-bottom: .3rem;
    display: flex;
    flex-direction: column;
    padding: .2rem .3rem .2rem .3rem;
    position: relative;
  }
  .mainItem {
    margin: .1rem 0 .1rem 0;
    display: flex;
    align-items: center;
    color: #aaa;
    font-size: 30rpx;
  }
  .itemType {
    width: 1.4rem!important;
    text-align: justify;
    text-align-last: justify;
  }
  .itemDetail {
    flex: 1;
    margin-left: .4rem;
  }

  .mainTel {
    height: .5rem;
    width: .5rem;
    background-size: cover;
    position: absolute;
    right: .3rem;
    top: 1.4rem;
    cursor: pointer;
  }
  .listTitle {
    height: .6rem;
    border-bottom: 1px solid rgba(0,0,0,.1);
    display: flex;
    align-items: center;
  }
  .titleLogo {
    margin-left: .3rem;
    display: flex;
    border: 1px solid #1E90FF;
    border-radius: 3px;
    font-size: 20rpx;
    color: #1E90FF;
    justify-content: center;
    align-items: center;
    padding: 0 .1rem 0 .1rem;
  }



</style>