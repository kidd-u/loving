<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor
      ref="resumeEditor"
      :markdown="currentMarkdown"
      :enableHtml="enableHtml"
    ></ResumeEditor>
  </div>
</template>
<script>
import StyleEditor from "./components/StyleEditor";
import ResumeEditor from "./components/ResumeEditor";
import "./assets/reset.css";
let isPc = (function () {
  var userAgentInfo = navigator.userAgent;
  var Agents = [
    "Android",
    "iPhone",
    "SymbianOS",
    "Windows Phone",
    "iPad",
    "iPod",
  ];
  var flag = true;
  for (var v = 0; v < Agents.length; v++) {
    if (userAgentInfo.indexOf(Agents[v]) > 0) {
      flag = false;
      break;
    }
  }
  return flag;
})();
let getDateDiff = function (startDate, endDate) {
  var startTime = new Date(Date.parse(startDate.replace(/-/g, "/"))).getTime();
  var endTime = new Date(Date.parse(endDate.replace(/-/g, "/"))).getTime();
  var dates = Math.abs(startTime - endTime) / (1000 * 60 * 60 * 24);
  return dates;
};
document.title +=
  getDateDiff(
    new Date().getFullYear() +
      "-" +
      (new Date().getMonth() + 1) +
      "-" +
      new Date().getDate(),
    "2012-08-31"
  ) +
  1 +
  "天";
export default {
  name: "app",
  components: {
    StyleEditor,
    ResumeEditor,
  },
  data() {
    return {
      interval: 27,
      currentStyle: "",
      enableHtml: false,
      fullStyle: [
        `/*
* Hi, YuanJiang!
* 终于把域名配置好了。发现了一个好玩的东东！
* 作为一名优秀的开发工程师。俗称程序员, 当然要部署了分享给你。
* 如这个页面。就是个什么也没有的网页。
* 现在让我来给这种空白的页面加点儿东西。
* 嗯。说起来手机和电脑还得区分一下。
* 你现在用的是。。。${isPc ? "电脑" : "手机"}
*/

/* 首先给所有元素加上过渡效果 */
* {
  -webkit-transition: all .3s;
  transition: all .3s;
}
/* 白色背景太单调了。来点背景 */
html {
  color: rgb(222,222,222);
  background: rgb(0,43,54); 
}
/* 文字太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  ${isPc ? "width: 48%;height: 96%;" : "width: 96%;height: 50%;"}
  font-size: 14px;
  line-height:1.5;
}
/* 这些代码颜色都一样。加点儿高亮区别来 */
.token.selector{ color: rgb(133,153,0) }
.token.property{ color: rgb(187,137,0) }
.token.punctuation{ color: yellow }
.token.function{ color: rgb(42,161,152) }
.token.comment{ color: rgb(177,177,177) }
/* 加个 3D 效果 */
html{
  -webkit-perspective: 1000px;
          perspective: 1000px;
}
.styleEditor {
  position: fixed; 
  ${isPc ? "left: 0;" : "left:0;right:0;margin:auto;"}
  top: 0; 
  -webkit-transition: none; 
  transition: none;   
  ${
    isPc
      ? "-webkit-transform: rotateY(10deg) translateZ(-100px) ;transform: rotateY(10deg) translateZ(-100px) ;"
      : "-webkit-transform: rotateX(-10deg) translateZ(-100px) ;transform: rotateX(-10deg) translateZ(-100px) ;"
  }
  ${
    isPc ? "" : "-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;"
  }
}

/* 再来一张信纸 */
.resumeEditor{
  position: fixed; 
  ${isPc ? "right: 0;" : "left:0;right:0;margin:auto;"}
  ${isPc ? "top: 0;" : "bottom:2%;"}
  padding: .5em;  
  ${isPc ? "margin: .5em;" : ""}
  ${isPc ? "width: 48%;height: 96%;" : "width: 96%;height: 50%;"}
  border: 1px solid;
  color: #222;
  overflow: auto;
  font-size: 14px;
  line-height:1.5;
  ${
    isPc
      ? "-webkit-transform: rotateY(-10deg) translateZ(-100px) ;transform: rotateY(-10deg) translateZ(-100px) ;"
      : "-webkit-transform: rotateX(10deg) translateZ(-100px) ;transform: rotateX(10deg) translateZ(-100px) ;"
  }
    ${
      isPc
        ? ""
        : "-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;"
    }
  }
/* 我开始写了 */


`,
        `
/* 是不是看着很简陋粗糙？
 * 因为这是 Markdown 格式的
 * 一种程序员用来写文档日志的简易语言
 * 翻译成 网页 就行了
 */
`,
        `
/* 再加点样式 */
.resumeEditor{
  padding: 2em;
  line-height:1.8;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
  font-size:18px;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;            
  content: counters(section, ".") " ";  
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: rgba(221,221,221,.5);
}

/* OK。完成！ */

`,
      ],
      currentMarkdown: "",
      fullMarkdown: `yvonne × kidd
----

2012年08月31日。初次见面。高一14班报道。  
去年在缘分的安排下，我们在一起了！  
已经相识 \`${
        getDateDiff(
          new Date().getFullYear() +
            "-" +
            (new Date().getMonth() + 1) +
            "-" +
            new Date().getDate(),
          "2012-08-31"
        ) + 1
      }\` 天

很开心收到来自三峡的明信片，这也是人生第一次收到信。哈哈哈，这将是我人生中最难忘记的回忆之一。

也祝我的YuanJiang可以开心快乐每一天！要爱自己呀！！！

> 【Screw the world × I have my dear YuanJiang】  
> 喂。我不只想和你有当下。过去，现在，未来，我们都要在一起！

`,
    };
  },
  created() {
    this.makeResume();
  },

  methods: {
    makeResume: async function () {
      await this.progressivelyShowStyle(0);
      await this.progressivelyShowResume();
      await this.progressivelyShowStyle(1);
      await this.showHtml();
      await this.progressivelyShowStyle(2);
    },
    showHtml: function () {
      return new Promise((resolve, reject) => {
        this.enableHtml = true;
        resolve();
      });
    },
    progressivelyShowStyle(n) {
      return new Promise((resolve, reject) => {
        let interval = this.interval;
        let showStyle = async function () {
          let style = this.fullStyle[n];
          if (!style) {
            return;
          }
          // 计算前 n 个 style 的字符总数
          let length = this.fullStyle
            .filter((_, index) => index <= n)
            .map((item) => item.length)
            .reduce((p, c) => p + c, 0);
          let prefixLength = length - style.length;
          if (this.currentStyle.length < length) {
            let l = this.currentStyle.length - prefixLength;
            let char = style.substring(l, l + 1) || " ";
            this.currentStyle += char;
            if (style.substring(l - 1, l) === "\n" && this.$refs.styleEditor) {
              this.$nextTick(() => {
                this.$refs.styleEditor.goBottom();
              });
            }
            setTimeout(showStyle, interval);
          } else {
            resolve();
          }
        }.bind(this);
        showStyle();
      });
    },
    progressivelyShowResume() {
      return new Promise((resolve, reject) => {
        let length = this.fullMarkdown.length;
        let interval = this.interval;
        let showResume = () => {
          if (this.currentMarkdown.length < length) {
            this.currentMarkdown = this.fullMarkdown.substring(
              0,
              this.currentMarkdown.length + 1
            );
            let lastChar =
              this.currentMarkdown[this.currentMarkdown.length - 1];
            let prevChar =
              this.currentMarkdown[this.currentMarkdown.length - 2];
            if (prevChar === "\n" && this.$refs.resumeEditor) {
              this.$nextTick(() => this.$refs.resumeEditor.goBottom());
            }
            setTimeout(showResume, interval);
          } else {
            resolve();
          }
        };
        showResume();
      });
    },
  },
};
</script>
<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

html {
  min-height: 100%;
}
.styleEditor {
  -webkit-backface-visibility: hidden;
}
</style>
