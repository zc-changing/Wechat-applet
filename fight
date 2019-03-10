// pages/fight/fight.js
//获取应用实例
//可以把这个js页面放到服务器上
var list = require('../../data/word.js')

const app = getApp()
Page({

  /**
   * 页面的初始数据
   */
  data: {
    completed: true,
    completed_A: false,//人工答题结束
    conpleted_B: false,
    countDown: 10,//倒计时
    isSearching: true,//寻找对手
    isReady: false,//开始对站前准备
    currentque:1,//当前提的索引
    score_A: 0,//人工得分
    score_B: 0,//机器得分
    gameover: false,//游戏结束
    userInfo: {},
    hasUserInfo: false,
    resultData:"",
    result:'',
    bc:"#000",
    bc_right: '#98FB98',
    bc_wrong: '#FF99B4',
    count:5,//题目总数
    
    length:""//单词的个数，
  
    
  },
//人工答题


  checkAns:function(e) {
   
  //console .log(e);
    let _this = this;
    
    let dataset = e.currentTarget.dataset;//获取答案text标签中的数据
   // console.log(dataset)
    let rightAns = dataset.right;//标准答案
    let index = dataset.index + 1;//人工选择的答案
     if (rightAns == index ) {
      
      _this.setData({
        score_A: _this.data.score_A + (_this.data.countDown) *1,
        
       })
     // console.log(_this.data.score_A)
     
    }
    else {
      console.log(false)
   
    }
    _this.setData({
      completed_A: true //只要答对此题就代表答题结束，进入下一题
    })
   
//判断人工答题是否结束
    if ((_this.data.completed_A == true || _this.data.complated_B == true) && _this.data.currentque <= list.day1.length) {
      _this.setData({
        completed: true,
        currentque: _this.data.currentque + 1,//开始设置下一题的索引
        countDown: 10,
    
      })
      clearInterval(getApp().globalData.timer1)//此题停止倒计时
      clearTimeout(getApp().globalData.timer2)
      _this.begin();//开始下一题
    } else{
       clearInterval(getApp().globalData.timer1)
    } 
    //显示比赛结果
    if (_this.data.currentque >= list.day1.length + 1) {
     
    
      _this.setData({
        currentque: list.day1.length,
        gameover: true,
      })
      clearInterval(getApp().globalData.timer1);
      console.log("最后一题了答题结束了！！！")
      console.log(_this.data.gameover)
      if (_this.data.score_A >= _this.data.score_B) {
        _this.setData({
          result: 'Win',
          resultData: getApp().globalData.userInfo.nickName + "赢得比赛"//直接显示头像
        })
        let nowgold = getApp().globalData.serData[0].ugold;
        getApp().globalData.serData[0].ugold = parseInt(nowgold) + parseInt(_this.data.prize)
      }
      else {
        _this.setData({
          result: 'Fail',
          resultData: "机器人赢得比赛"//获取机器人头像去替换
        })
      }
      /* let timer5 = setTimeout(()=>{
         wx.redirectTo({
           url: '../session/session',
         })
         // console.log(getApp().globalData)
         clearTimeout(timer5);
         clearInterval(getApp().globalData.timer1)
       },1000)*/
    }

    
  /* else if(_this.data.currentque==_this.data.cout - 1){
     //已经做完最后一题
      clearInterval(getApp().globalData.timer1);//此题停止倒计时
      _this.setData({
        gameover:true
      });
      if(_this.data.scoreA>_this.data.scoreB){
        _this.setData({
          result:'win',
          resultData: getApp().globalData.userInfo.nickName +"赢得比赛"
        });
      }else{
        _this.setData({
          result:"Fail",
          resultData:"机器人赢得比赛"
        });
      }

   } */
    var word = list.day1[_this.data.currentque - 1]
    //console.log("想看把" +list.{{data1}} )
    _this.setData({
      que: word.que,
      ans: word.ans,
      right: word.right
   

    })

  },
  

//机器答题
  getRandom:function(min, max) {
    return min + Math.floor(Math.random() * (max - min + 1));
  },

//机器人答题
  runRobat:function() {
    let _this = this;
    var word = list.day1[_this.data.currentque - 1]
    //console.log('length是' + list.day1.length)
    let random = _this.getRandom(2, 5);//调用getrandom函数
    let right =word.right;
    let rightRandom = _this.getRandom(1, 10);
    //console.log("随机数："+rightRandom)
    let timer4 = setTimeout(() => {
      if (rightRandom < 5) {
        console.log('right')
        _this.setData({
          score_B: _this.data.score_B + (_this.data.countDown) * 1
        })
      }
      else {
        console.log('wrong')
      }

     /* _this.setData({
        completed_B: true,
      })*/
     
      //判断答题结束先试下一题,,,,《改变条件中的数字以至于出更多的题  list.day1.length》
      if ((_this.data.completed_A == true || _this.data.completed_B == true) && _this.data.currentque < list.day1.length + 1) {
        _this.setData({
          completed: true,
           currentque: _this.data.currentque + 1,
          countDown: 10
        })
        clearInterval(getApp().globalData.timer1)
        clearTimeout(getApp().globalData.timer2)
        clearTimeout(timer4)
        _this.begin();
      }

    }, random * 1000)
    console.log(random, right)
  },

//对战开始函数
  begin:function() {
    let _this = this;
    
    _this.setData({
      completed: false,
      completed_A: false,
      completed_B: false,
      countDown: 10
    })
    var word = list.day1[_this.data.currentque - 1]
    //console.log("在这里" +[_this.data.currentque + 1]),
    //console.log("word是" + word.que)
    _this.setData({
      que: word.que,
      ans: word.ans,
      right: word.right

    })
    _this.setData({
      que: word.que,
      ans: word.ans,
      right: word.right

    })
//改变下面的数字大小，显示更多的题  list.day1.length
    if (_this.data.currentque <= list.day1.length + 1 && _this.data.gameover==false) {

      _this.runRobat();//调用Runrobat函数
     
      getApp().globalData.timer1 = setInterval(function(){//setInterval() 方法可按照指定的周期（以毫秒计）来调用函数或计算表达式。
     
        _this.setData({
          countDown: _this.data.countDown - 1,
         
        })
        //console.log(this.data.countDown)
     
        if (_this.data.countDown ==1) {
        _this.data.completed = true;
          clearInterval(getApp().globalData.timer1);
       
          getApp().globalData.timer2 = setTimeout(function () {
            _this.begin();
            _this.setData({
              currentque: _this.data.currentque + 1
            })
            clearInterval(getApp().globalData.timer2)
          }, 1000)
        }
        console.log(333)
      }, 1000)
    }else{
      
        clearInterval(getApp().globalData.timer1);

    }
    


  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    console.log('onLoad')
   
    var that = this
    //调用应用实例的方法获取全局数据
    app.getUserInfo(function (userInfo) {
      //更新数据
      that.setData({
        userInfo: userInfo
      })
    })
  

  },

 

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {
    let _this = this;
    //定时器从寻找对手界面到对战准备的界面
    setTimeout(() => {
      _this.setData({
        isSearching: false,
      })
    }, 2000)
     
     //进入到对战状态
    setTimeout(() => {
      _this.setData({
        isReady: true
      })
     
      _this.begin();//开始游戏
    }, 3000)
  }

})


