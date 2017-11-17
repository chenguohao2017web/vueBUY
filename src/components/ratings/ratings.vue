<template>
  <div class="ratings" ref="ratingsWrapper">
      <div class="ratings_content">
        <div class="ratings_score">
          <div class="ratings_score_left">
            <h1 class="score">{{seller.score}}</h1>
            <p class="text">综合评分</p>
            <p class="rankRate">高于周边商家{{seller.rankRate}}%</p>
          </div>
          <div class="ratings_score_right">
            <div class="score_wrapper">
              <span class="title">服务态度</span>
              <star></star>
              <span class="score_num">{{seller.serviceScore}}</span>
            </div>
            <div class="score_wrapper">
              <span class="title">服务态度</span>
              <star></star>
              <span class="score_num">{{seller.serviceScore}}</span>
            </div>
            <div class="delivery_wrapper">
              <span class="title">送达时间</span>
              <span class="time">{{seller.deliveryTime}}</span>
            </div>
          </div>
        </div>
        <split></split>
        <ratingSelect
        :ratings="ratings"
        :selectType="selectType"
        :viewHasContent="viewHasContent"
        @selectTypeEvent="changeSelectType"
        @viewHasContentEvent="changeViewHasContent"
        ></ratingSelect>

        <div class="ratings_content_wrapper">
            <ul>
              <li v-for="rating in ratings" class="rating_item" v-show="selectRating(rating.rateType,rating.text)">
                <div class="avatar">
                  <img :src="rating.avatar" alt="" width="24px" height="24px">
                </div>
                <div class="rating_content">
                  <h1 class="username">{{rating.username}}</h1>
                  <div class="starWrapper"><star :score="rating.score"></star></div>
                  <span v-show="rating.deliveryTime" class="deliveryTime">{{rating.deliveryTime}}分钟送达</span>
                  <p class="text" v-show="rating.text">{{rating.text}}</p>
                  <div>
                    <span class="icon" :class="{on:rating.rateType==1}"></span>
                    <span v-show="rating.recommend" v-for="item in rating.recommend" class="recomment_item">{{item}}</span>
                  </div>
                </div>
                <div class="now_time">
                  {{rating.rateTime | changeTime}}
                </div>
              </li>
            </ul>
        </div>
      </div>
  </div>
</template>
<script>
const data = {
  seller: {
    name: "粥品香坊（回龙观）",
    description: "蜂鸟专送",
    deliveryTime: 38,
    score: 3.5,
    serviceScore: 4.1,
    foodScore: 4.3,
    rankRate: 69.2,
    minPrice: 20,
    deliveryPrice: 4,
    ratingCount: 24,
    sellCount: 90,
    bulletin:
      "粥品香坊其烹饪粥料的秘方源于中国千年古法，在融和现代制作工艺，由世界烹饪大师屈浩先生领衔研发。坚守纯天然、0添加的良心品质深得消费者青睐，发展至今成为粥类的引领品牌。是2008年奥运会和2013年园博会指定餐饮服务商。",
    supports: [
      {
        type: 0,
        description: "在线支付满28减5"
      },
      {
        type: 1,
        description: "VC无限橙果汁全场8折"
      },
      {
        type: 2,
        description: "单人精彩套餐"
      },
      {
        type: 3,
        description: "该商家支持发票,请下单写好发票抬头"
      },
      {
        type: 4,
        description: "已加入“外卖保”计划,食品安全保障"
      }
    ],
    avatar:
      "http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg",
    pics: [
      "http://fuss10.elemecdn.com/8/71/c5cf5715740998d5040dda6e66abfjpeg.jpeg?imageView2/1/w/180/h/180",
      "http://fuss10.elemecdn.com/b/6c/75bd250e5ba69868f3b1178afbda3jpeg.jpeg?imageView2/1/w/180/h/180",
      "http://fuss10.elemecdn.com/f/96/3d608c5811bc2d902fc9ab9a5baa7jpeg.jpeg?imageView2/1/w/180/h/180",
      "http://fuss10.elemecdn.com/6/ad/779f8620ff49f701cd4c58f6448b6jpeg.jpeg?imageView2/1/w/180/h/180"
    ],
    infos: [
      "该商家支持发票,请下单写好发票抬头",
      "品类:其他菜系,包子粥店",
      "北京市昌平区回龙观西大街龙观置业大厦底商B座102单元1340",
      "营业时间:10:00-20:30"
    ]
  },
  goods: [
    {
      name: "热销榜",
      type: -1,
      foods: [
        {
          name: "皮蛋瘦肉粥",
          price: 10,
          oldPrice: "",
          description: "咸粥",
          sellCount: 229,
          rating: 100,
          info:
            "一碗皮蛋瘦肉粥，总是我到粥店时的不二之选。香浓软滑，饱腹暖心，皮蛋的Q弹与瘦肉的滑嫩伴着粥香溢于满口，让人喝这样的一碗粥也觉得心满意足",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "很喜欢的粥",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 1,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/c/cd/c12745ed8a5171e13b427dbc39401jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/c/cd/c12745ed8a5171e13b427dbc39401jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "扁豆焖面",
          price: 14,
          oldPrice: "",
          description: "",
          sellCount: 188,
          rating: 96,
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 1,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          info: "",
          icon:
            "http://fuss10.elemecdn.com/c/6b/29e3d29b0db63d36f7c500bca31d8jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/c/6b/29e3d29b0db63d36f7c500bca31d8jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "葱花饼",
          price: 10,
          oldPrice: "",
          description: "",
          sellCount: 124,
          rating: 85,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 1,
              text: "没啥味道",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 1,
              text: "很一般啊",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "牛肉馅饼",
          price: 14,
          oldPrice: "",
          description: "",
          sellCount: 114,
          rating: 91,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 1,
              text: "难吃不推荐",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/d/b9/bcab0e8ad97758e65ae5a62b2664ejpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/d/b9/bcab0e8ad97758e65ae5a62b2664ejpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "招牌猪肉白菜锅贴/10个",
          price: 17,
          oldPrice: "",
          description: "",
          sellCount: 101,
          rating: 78,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 1,
              text: "不脆,不好吃",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/7/72/9a580c1462ca1e4d3c07e112bc035jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/7/72/9a580c1462ca1e4d3c07e112bc035jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "南瓜粥",
          price: 9,
          oldPrice: "",
          description: "甜粥",
          sellCount: 91,
          rating: 100,
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/8/a6/453f65f16b1391942af11511b7a90jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/8/a6/453f65f16b1391942af11511b7a90jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "红豆薏米美肤粥",
          price: 12,
          oldPrice: "",
          description: "甜粥",
          sellCount: 86,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/d/22/260bd78ee6ac6051136c5447fe307jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/d/22/260bd78ee6ac6051136c5447fe307jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "八宝酱菜",
          price: 4,
          oldPrice: "",
          description: "",
          sellCount: 84,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/9/b5/469d8854f9a3a03797933fd01398bjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/9/b5/469d8854f9a3a03797933fd01398bjpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "红枣山药糙米粥",
          price: 10,
          oldPrice: "",
          description: "",
          sellCount: 81,
          rating: 91,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/9/b5/469d8854f9a3a03797933fd01398bjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/9/b5/469d8854f9a3a03797933fd01398bjpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "糊塌子",
          price: 10,
          oldPrice: "",
          description: "",
          sellCount: 80,
          rating: 93,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/0/05/097a2a59fd2a2292d08067e16380cjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/0/05/097a2a59fd2a2292d08067e16380cjpeg.jpeg?imageView2/1/w/750/h/750"
        }
      ]
    },
    {
      name: "单人精彩套餐",
      type: 2,
      foods: [
        {
          name: "红枣山药粥套餐",
          price: 29,
          oldPrice: 36,
          description: "红枣山药糙米粥",
          sellCount: 17,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/6/72/cb844f0bb60c502c6d5c05e0bddf5jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/6/72/cb844f0bb60c502c6d5c05e0bddf5jpeg.jpeg?imageView2/1/w/750/h/750"
        }
      ]
    },
    {
      name: "冰爽饮品限时特惠",
      type: 1,
      foods: [
        {
          name: "VC无限橙果汁",
          price: 8,
          oldPrice: 10,
          description: "",
          sellCount: 15,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "还可以",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/e/c6/f348e811772016ae24e968238bcbfjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/e/c6/f348e811772016ae24e968238bcbfjpeg.jpeg?imageView2/1/w/750/h/750"
        }
      ]
    },
    {
      name: "精选热菜",
      type: -1,
      foods: [
        {
          name: "娃娃菜炖豆腐",
          price: 17,
          oldPrice: "",
          description: "",
          sellCount: 43,
          rating: 92,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "菜量还可以,味道还可以",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/d/2d/b1eb45b305635d9dd04ddf157165fjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/d/2d/b1eb45b305635d9dd04ddf157165fjpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "手撕包菜",
          price: 16,
          oldPrice: "",
          description: "",
          sellCount: 29,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/9/c6/f3bc84468820121112e79583c24efjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/9/c6/f3bc84468820121112e79583c24efjpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "香酥黄金鱼/3条",
          price: 11,
          oldPrice: "",
          description: "",
          sellCount: 15,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/4/e7/8277a6a2ea0a2e97710290499fc41jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/4/e7/8277a6a2ea0a2e97710290499fc41jpeg.jpeg?imageView2/1/w/750/h/750"
        }
      ]
    },
    {
      name: "爽口凉菜",
      type: -1,
      foods: [
        {
          name: "八宝酱菜",
          price: 4,
          oldPrice: "",
          description: "",
          sellCount: 84,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/9/b5/469d8854f9a3a03797933fd01398bjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/9/b5/469d8854f9a3a03797933fd01398bjpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "拍黄瓜",
          price: 9,
          oldPrice: "",
          description: "",
          sellCount: 28,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/6/54/f654985b4e185f06eb07f8fa2b2e8jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/6/54/f654985b4e185f06eb07f8fa2b2e8jpeg.jpeg?imageView2/1/w/750/h/750"
        }
      ]
    },
    {
      name: "精选套餐",
      type: -1,
      foods: [
        {
          name: "红豆薏米粥套餐",
          price: 37,
          oldPrice: "",
          description: "红豆薏米粥,三鲜干蒸烧卖,拍黄瓜",
          sellCount: 3,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/f/49/27f26ed00c025b2200a9ccbb7e67ejpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/f/49/27f26ed00c025b2200a9ccbb7e67ejpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "皮蛋瘦肉粥套餐",
          price: 31,
          oldPrice: "",
          description: "",
          sellCount: 12,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/8/96/f444a8087f0e940ef264617f9d98ajpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/8/96/f444a8087f0e940ef264617f9d98ajpeg.jpeg?imageView2/1/w/750/h/750"
        }
      ]
    },
    {
      name: "果拼果汁",
      type: -1,
      foods: [
        {
          name: "蜜瓜圣女萝莉杯",
          price: 6,
          oldPrice: "",
          description: "",
          sellCount: 1,
          rating: "",
          info: "",
          ratings: [],
          icon:
            "http://fuss10.elemecdn.com/b/5f/b3b04c259d5ec9fa52e1856ee50dajpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/b/5f/b3b04c259d5ec9fa52e1856ee50dajpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "加多宝",
          price: 6,
          oldPrice: "",
          description: "",
          sellCount: 7,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/b/9f/5e6c99c593cf65229225c5661bcdejpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/b/9f/5e6c99c593cf65229225c5661bcdejpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "VC无限橙果汁",
          price: 8,
          oldPrice: 10,
          description: "",
          sellCount: 15,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "还可以",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/e/c6/f348e811772016ae24e968238bcbfjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/e/c6/f348e811772016ae24e968238bcbfjpeg.jpeg?imageView2/1/w/750/h/750"
        }
      ]
    },
    {
      name: "小吃主食",
      type: -1,
      foods: [
        {
          name: "扁豆焖面",
          price: 14,
          oldPrice: "",
          description: "",
          sellCount: 188,
          rating: 96,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 1,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/c/6b/29e3d29b0db63d36f7c500bca31d8jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/c/6b/29e3d29b0db63d36f7c500bca31d8jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "葱花饼",
          price: 10,
          oldPrice: "",
          description: "",
          sellCount: 124,
          rating: 85,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 1,
              text: "没啥味道",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 1,
              text: "很一般啊",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/f/28/a51e7b18751bcdf871648a23fd3b4jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "牛肉馅饼",
          price: 14,
          oldPrice: "",
          description: "",
          sellCount: 114,
          rating: 91,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 1,
              text: "难吃不推荐",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/d/b9/bcab0e8ad97758e65ae5a62b2664ejpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/d/b9/bcab0e8ad97758e65ae5a62b2664ejpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "招牌猪肉白菜锅贴/10个",
          price: 17,
          oldPrice: "",
          description: "",
          sellCount: 101,
          rating: 78,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 1,
              text: "不脆,不好吃",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/7/72/9a580c1462ca1e4d3c07e112bc035jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/7/72/9a580c1462ca1e4d3c07e112bc035jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "糊塌子",
          price: 10,
          oldPrice: "",
          description: "",
          sellCount: 80,
          rating: 93,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/0/05/097a2a59fd2a2292d08067e16380cjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/0/05/097a2a59fd2a2292d08067e16380cjpeg.jpeg?imageView2/1/w/750/h/750"
        }
      ]
    },
    {
      name: "特色粥品",
      type: -1,
      foods: [
        {
          name: "皮蛋瘦肉粥",
          price: 10,
          oldPrice: "",
          description: "咸粥",
          sellCount: 229,
          rating: 100,
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "很喜欢的粥",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 1,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/c/cd/c12745ed8a5171e13b427dbc39401jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/c/cd/c12745ed8a5171e13b427dbc39401jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "南瓜粥",
          price: 9,
          oldPrice: "",
          description: "甜粥",
          sellCount: 91,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/8/a6/453f65f16b1391942af11511b7a90jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/8/a6/453f65f16b1391942af11511b7a90jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "红豆薏米美肤粥",
          price: 12,
          oldPrice: "",
          description: "甜粥",
          sellCount: 86,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/d/22/260bd78ee6ac6051136c5447fe307jpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/d/22/260bd78ee6ac6051136c5447fe307jpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "红枣山药糙米粥",
          price: 10,
          oldPrice: "",
          description: "",
          sellCount: 81,
          rating: 91,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/9/b5/469d8854f9a3a03797933fd01398bjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/9/b5/469d8854f9a3a03797933fd01398bjpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "鲜蔬菌菇粥",
          price: 11,
          oldPrice: "",
          description: "咸粥",
          sellCount: 56,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: ""
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/e/a3/5317c68dd618929b6ac05804e429ajpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/e/a3/5317c68dd618929b6ac05804e429ajpeg.jpeg?imageView2/1/w/750/h/750"
        },
        {
          name: "田园蔬菜粥",
          price: 10,
          oldPrice: "",
          description: "咸粥",
          sellCount: 33,
          rating: 100,
          info: "",
          ratings: [
            {
              username: "3******c",
              rateTime: 1469281964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "2******3",
              rateTime: 1469271264000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            },
            {
              username: "3******b",
              rateTime: 1469261964000,
              rateType: 0,
              text: "",
              avatar:
                "http://static.galileo.xiaojukeji.com/static/tms/default_header.png"
            }
          ],
          icon:
            "http://fuss10.elemecdn.com/a/94/7371083792c19df00e546b29e344cjpeg.jpeg?imageView2/1/w/114/h/114",
          image:
            "http://fuss10.elemecdn.com/a/94/7371083792c19df00e546b29e344cjpeg.jpeg?imageView2/1/w/750/h/750"
        }
      ]
    }
  ],
  ratings: [
    {
      username: "3******c",
      rateTime: 1469281964000,
      deliveryTime: 30,
      score: 5,
      rateType: 0,
      text: "不错,粥很好喝,我经常吃这一家,非常赞,以后也会常来吃,强烈推荐.",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: ["南瓜粥", "皮蛋瘦肉粥", "扁豆焖面", "娃娃菜炖豆腐", "牛肉馅饼"]
    },
    {
      username: "2******3",
      rateTime: 1469271264000,
      deliveryTime: "",
      score: 4,
      rateType: 0,
      deliveryTime: "",
      text: "服务态度不错",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: ["扁豆焖面"]
    },
    {
      username: "3******b",
      rateTime: 1469261964000,
      score: 3,
      rateType: 1,
      text: "",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "1******c",
      rateTime: 1469261864000,
      deliveryTime: 20,
      score: 5,
      rateType: 0,
      text: "良心店铺",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "2******d",
      rateTime: 1469251264000,
      deliveryTime: 10,
      score: 4,
      rateType: 0,
      text: "",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "9******0",
      rateTime: 1469241964000,
      deliveryTime: 70,
      score: 1,
      rateType: 1,
      text: "送货速度蜗牛一样",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "d******c",
      rateTime: 1469231964000,
      deliveryTime: 30,
      score: 5,
      rateType: 0,
      text: "很喜欢的粥店",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "2******3",
      rateTime: 1469221264000,
      deliveryTime: "",
      score: 4,
      rateType: 0,
      text: "量给的还可以",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "3******8",
      rateTime: 1469211964000,
      deliveryTime: "",
      score: 3,
      rateType: 1,
      text: "",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "a******a",
      rateTime: 1469201964000,
      deliveryTime: "",
      score: 4,
      rateType: 0,
      text: "孩子喜欢吃这家",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: ["南瓜粥"]
    },
    {
      username: "3******3",
      rateTime: 1469191264000,
      deliveryTime: "",
      score: 4,
      rateType: 0,
      text: "粥挺好吃的",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "t******b",
      rateTime: 1469181964000,
      deliveryTime: "",
      score: 3,
      rateType: 1,
      text: "",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "f******c",
      rateTime: 1469171964000,
      deliveryTime: 15,
      score: 5,
      rateType: 0,
      text: "送货速度很快",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "k******3",
      rateTime: 1469161264000,
      deliveryTime: "",
      score: 4,
      rateType: 0,
      text: "",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "u******b",
      rateTime: 1469151964000,
      deliveryTime: "",
      score: 4,
      rateType: 0,
      text: "下雨天给快递小哥点个赞",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "s******c",
      rateTime: 1469141964000,
      deliveryTime: "",
      score: 4,
      rateType: 0,
      text: "好",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "z******3",
      rateTime: 1469131264000,
      deliveryTime: "",
      score: 5,
      rateType: 0,
      text: "吃了还想再吃",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "n******b",
      rateTime: 1469121964000,
      deliveryTime: "",
      score: 3,
      rateType: 1,
      text: "发票开的不对",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "m******c",
      rateTime: 1469111964000,
      deliveryTime: 30,
      score: 5,
      rateType: 0,
      text: "好吃",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "l******3",
      rateTime: 1469101264000,
      deliveryTime: 40,
      score: 5,
      rateType: 0,
      text: "还不错吧",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "3******o",
      rateTime: 1469091964000,
      deliveryTime: "",
      score: 2,
      rateType: 1,
      text: "",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "3******p",
      rateTime: 1469081964000,
      deliveryTime: "",
      score: 4,
      rateType: 0,
      text: "很喜欢的粥",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "o******k",
      rateTime: 1469071264000,
      deliveryTime: "",
      score: 5,
      rateType: 0,
      text: "",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    },
    {
      username: "k******b",
      rateTime: 1469061964000,
      deliveryTime: "",
      score: 4,
      rateType: 0,
      text: "",
      avatar:
        "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
      recommend: []
    }
  ]
};
const ratings = data.ratings;
import Bscroll from "better-scroll";
import ratingSelect from "../ratingselect/ratingselect";
import split from "../split/split";
import star from "../star/star";
export default {
  data() {
    return {
      selectType: 2,
      viewHasContent: false
    };
  },
  props: {
    seller: {
      type: Object,
      ratings: []
    }
  },
  components: { star, split, ratingSelect },
  created() {
    this.ratings = ratings;
    this.$nextTick(() => {
      this.ratingsWrapper = new Bscroll(this.$refs.ratingsWrapper, {
        click: true
      });
    });
  },
  filters: {
    changeTime(time) {
      var date = new Date(time);
      var sYear = date.getFullYear() + "";
      var sMonth = date.getMonth() + 1 + "";
      var sDay = date.getDay() + "";
      var sHours = date.getHours() + "";
      var sMinutes = date.getMinutes() + "";
      var sSeconds = date.getSeconds() + "";
      return sYear + "-" + sMonth + "-" + sDay + " " + sHours + ":" + sMinutes;
    }
  },
  methods: {
    selectRating(type, text) {
      // 0推荐 1:踩，2全部，
      if (this.viewHasContent && !text) {
        // 如果只看有内容按钮为on 并且 文本内容为空时 这个li不展示
        return false;
      }
      //内容按钮为false  并且类型全部
      if (this.selectType == 2) {
        return true;
      } else {
        return this.selectType == type;
      }
    },
    changeSelectType(type) {
      this.selectType = type;
      this.$nextTick(()=>{
        this.ratingsWrapper.refresh();
      })
    },
    changeViewHasContent(bool) {
      this.viewHasContent = bool;
      this.$nextTick(()=>{
        this.ratingsWrapper.refresh();
      })
    }
  }
};
</script>
<style lang="less">
.ratings {
  position: absolute;
  left: 0;
  top: 162px;
  bottom: 0;
  width: 100%;
  overflow: hidden;

  .ratings_score {
    padding: 18px 0;
    display: flex;

    .ratings_score_left {
      flex: 0 0 137px;
      width: 137px;
      text-align: center;
      border-right: 1px solid #eee;
      @media screen and (max-width: 320px) {
        flex: 0 0 100px;
        width: 100px;
      }
      .score {
        font-size: 24px;
        color: rgb(255, 153, 0);
        line-height: 28px;
      }
      .text {
        font-size: 12px;
        color: rgb(7, 17, 27);
        line-height: 12px;
        padding-top: 6px;
      }
      .rankRate {
        padding-top: 8px;
        font-size: 10px;
        color: #ccc;
        line-height: 12px;
      }
    }
    .ratings_score_right {
      flex: 1;
      padding-left: 24px;
      @media screen and (max-width: 320px) {
        padding-left: 10px;
      }
      .score_wrapper > * {
        display: inline-block;
      }
      .score_wrapper {
        font-size: 0;
        .score_num {
          font-size: 12px;
          color: rgb(255, 153, 0);
          line-height: 18px;
          vertical-align: top;
          padding-left: 12px;
        }
      }
      .title {
        vertical-align: top;
        line-height: 18px;
        padding-bottom: 8px;
        margin-right: 12px;
        font-size: 12px;
        color: rgb(7, 17, 27);
        &:last-child {
          padding-bottom: 0;
        }
      }
      .delivery_wrapper {
        font-size: 0;
        span {
          display: inline-block;
        }
        .time {
          font-size: 12px;
          line-height: 18px;
          color: rgb(147, 153, 159);
        }
      }
    }
  }
  .ratings_content_wrapper {
    padding: 0 18px;

    .rating_item {
      padding: 18px 0;
      display: flex;
      position: relative;
      .now_time {
        position: absolute;
        top: 18px;
        right: 0;
        font-size: 12px;
        color: rgb(147, 153, 159);
        line-height: 12px;
      }
      .avatar {
        flex: 0 0 24px;
        width: 24px;
      }
      .rating_content {
        flex: 1;
        padding-left: 12px;
        .icon {
          display: inline-block;
          width: 20px;
          height: 20px;
          background: url("../../assets/赞.png") no-repeat center;
          background-size: 100%;
          margin-right: 4px;
          &.on {
            background: url("../../assets/踩.png") no-repeat center;
            background-size: 100%;
          }
        }
        .username {
          font-size: 10px;
          color: rgb(7, 17, 27);
          line-height: 12px;
          padding-bottom: 4px;
        }
        .starWrapper {
          display: inline-block;
        }
        .deliveryTime {
          font-size: 10px;
          font-weight: 200;
          color: rgb(147, 153, 159);
          line-height: 22px;
          display: inline-block;
          height: 22px;
          vertical-align: top;
        }
        .text {
          padding: 6px 0 8px 0;
          font-size: 12px;
          color: rgb(7, 17, 27);
          line-height: 18px;
        }
        .recomment_item {
          display: inline-block;
          overflow: hidden;
          text-overflow: ellipsis;
          text-align: center;
          padding: 2px 6px;
          border: 1px solid #eee;
          margin-right: 8px;
          font-size: 10px;
          color: rgb(147, 153, 159);
        }
      }
    }
  }
}
</style>

