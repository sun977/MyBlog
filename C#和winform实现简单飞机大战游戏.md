### C#和winform实现简单飞机大战游戏



### 目录

- - - [C#和winform实现简单飞机大战游戏](https://blog.csdn.net/weixin_42742658/article/details/105567972#Cwinform_0)

    - - [前言](https://blog.csdn.net/weixin_42742658/article/details/105567972#_2)

      - [类和对象的思维导图](https://blog.csdn.net/weixin_42742658/article/details/105567972#_4)

      - [各个类的详解](https://blog.csdn.net/weixin_42742658/article/details/105567972#_7)

      - - [1、GameObject类【所有游戏对象的父类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#1GameObject_8)
        - [2、BackGround ： GameObject【背景类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#2BackGround__GameObject_23)
        - [3、PlaneFather ： GameObject【所有飞机的父类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#3PlaneFather__GameObject_32)
        - [4、PlaneHero ： PlaneFather【玩家飞机类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#4PlaneHero__PlaneFather_42)
        - [5、PlaneEnemy ：PlaneFather【敌人飞机类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#5PlaneEnemy_PlaneFather_53)
        - [6、ZiDan ：GameObject【所有子弹的父类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#6ZiDan_GameObject_71)
        - [7、HeroZiDan ：ZiDan【玩家子飞机弹类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#7HeroZiDan_ZiDan_81)
        - [8、EnemyZiDan ：ZiDan【敌人飞机子弹类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#8EnemyZiDan_ZiDan_89)
        - [9、Boom ：GameObject【所有爆炸效果父类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#9Boom_GameObject_96)
        - [10、HeroBoom : Boom【玩家飞机爆炸类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#10HeroBoom__Boom_102)
        - [11、EnemyBoom : Boom【敌人飞机爆炸类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#11EnemyBoom__Boom_111)
        - [12、SingleObject ：GameObject【单例类】](https://blog.csdn.net/weixin_42742658/article/details/105567972#12SingleObject_GameObject_123)

      - [成品代码](https://blog.csdn.net/weixin_42742658/article/details/105567972#_142)

      - - [Form1.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#Form1cs_144)
        - [GameObject.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#GameObjectcs_272)
        - [BackGround.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#BackGroundcs_451)
        - [PlaneFather.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#PlaneFathercs_489)
        - [PlaneHero.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#PlaneHerocs_526)
        - [PlaneEnemy.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#PlaneEnemycs_585)
        - [ZiDan.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#ZiDancs_804)
        - [HeroZiDan.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#HeroZiDancs_873)
        - [EnemyZiDan.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#EnemyZiDancs_898)
        - [Boom.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#Boomcs_922)
        - [HeroBoom.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#HeroBoomcs_942)
        - [EnemyBoom.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#EnemyBoomcs_983)
        - [SingleObject.cs](https://blog.csdn.net/weixin_42742658/article/details/105567972#SingleObjectcs_1071)

      - [小结](https://blog.csdn.net/weixin_42742658/article/details/105567972#_1316)



#### 前言

作为学习C#的一个阶段的总结，我在网络上找寻一些资源，加上自己的一些思考完成了这个飞机大战游戏1.0版本，游戏本身还有很多bug，后续有时间会继续完善。游戏很经典，网上相关的材料也很多，但是代码是我经过思考学习，自己完成的。有需要的伙伴们可以分享，编程大牛勿喷，我还是个菜j。

#### 类和对象的思维导图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200416215304457.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

#### 各个类的详解

##### 1、GameObject类【所有游戏对象的父类】

```
属性：
     X ：横坐标
     Y ：纵坐标
     Width ：宽度
     Heigth ：高度
     Speed ：速度
     Life ：生命值
     Dirction ：方向
方法：
     Move() ：移动虚方法
     Draw() ：绘制到窗体的抽象方法
     GetRectangle() ：用于碰撞检测的方法
```

##### 2、BackGround ： GameObject【背景类】

```
 属性：
     imgBG：背景图片
 方法：
     BackGround()：调用GameOblect类的构造函数
     Draw()：绘制自己到窗体
12345
```

##### 3、PlaneFather ： GameObject【所有飞机的父类】

```
属性：
     imgPlane ：存放飞机图片变量
方法：
     PlaneFather() ：构造函数，调用GameObject的构造函数
     Fire() ：开火，抽象方法
     IsOver() ：死亡，抽象方法
```

##### 4、PlaneHero ： PlaneFather【玩家飞机类】

```
属性：
     imgHero ：存放玩家飞机图片
方法：
     PlaneHero() ：构造函数调用飞机父类构造函数
     Draw() : 绘制自己到窗体方法
     MouseMove() ：跟随鼠标移动方法
     Fire() ：开火方法 重写
     IsOver() ：死亡方法 重写
```

##### 5、PlaneEnemy ：PlaneFather【敌人飞机类】

```
属性：
    img1 ：小飞机
    img2 ：中飞机
    img3 ：大飞机
    EnemyType ：飞机类型
方法：
    PlaneEnemy() ：构造函数
    GetImage() ：根据类型返回飞机图片方法
    GetLife() ：根据类型返回飞机生命值方法
    GetSpeed() ：根据类型返回飞机速度方法
    Draw() ：绘制自己到窗体的方法
    Move() ：移动方法 重写
    Fire() ：开火方法 重写
    IsOver() ：死亡方法 重写
```

##### 6、ZiDan ：GameObject【所有子弹的父类】

```
属性：
     imgZiDan ：子弹图片变量
     Power ：子弹威力变量
方法：
     ZiDan() ：构造函数
     Draw() ：绘制自己到窗体的方法
     Move() ：移动方法 重写
```

##### 7、HeroZiDan ：ZiDan【玩家子飞机弹类】

```
属性：
     imgHero ：玩家子弹图片变量
方法：
     HeroZiDan ：构造函数
```

##### 8、EnemyZiDan ：ZiDan【敌人飞机子弹类】

```
属性：
    imgHero ：敌人子弹图片变量
方法：
    HeroZiDan ：构造函数
```

##### 9、Boom ：GameObject【所有爆炸效果父类】

```
属性：
方法：
  Boom() ：构造函数
```

##### 10、HeroBoom : Boom【玩家飞机爆炸类】

```
属性：
   imgs[] ：存放玩家飞机爆炸图片的数组
  方法：
   HeroBoom() ：构造函数
   Draw() ：绘制自己到窗体的方法 重写
```

##### 11、EnemyBoom : Boom【敌人飞机爆炸类】

```
属性：
   imgs1[] ：小飞机爆炸图片数组
   imgs2[] ：中飞机爆炸图片数字
   imgs3[] ：大飞机爆炸图片数组
   Type ：飞机类型
  方法：
   EnemyBoom() ：构造函数
   Draw() ：绘制自己到窗体的方法
```

##### 12、SingleObject ：GameObject【单例类】

```
    属性：
     single
     Score ： 用于记分的变量
     BackGround ：背景对象
     PH ：玩家飞机对象
     listHearoZiDan ：玩家飞机子弹集合对象
     listEnemyZiDan ：敌人飞机子弹集合对象
     listPlaneEnemy ：敌人飞机集合对象
     listEnemyBoom ：敌人飞机爆炸对象
     listHeroBoom ：玩家飞机爆炸对象
    方法：
      AddGameObject() ：添加游戏对象到窗体
      RemoveGameObject() ：从窗体移除游戏对象
      Draw() ：调用对象本身的Draw()函数绘制对象本身
      Collision() ：碰撞检测方法
```

#### 成品代码

##### Form1.cs

```
Form1.cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace 飞机大战_2020
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
            InitialGame();//调用初始化函数
        }

        static Random r = new Random();//用于随机出现敌人飞机，用于限制飞机出现的几率

        // 初始化游戏
        public void InitialGame()
        {
            //首先初始化背景
            SingleObject.GetSingle().AddGameObject(new BackGround(0,-850,5));

            //初始化玩家飞机
            SingleObject.GetSingle().AddGameObject(new PlaneHero(160, 550, 5, 3, Direction.Up));

            //初始化敌人飞机，敌人飞机众多，所以单写一个函数来初始化
            InitialPlaneEnemy();
            
        }

        //初始化敌人飞机需要timer实时判断数量并重新初始化
        private void InitialPlaneEnemy()
        {
            for (int i = 0; i < 4; i++)//循环出现敌人飞机 4后面可以设置
            {
                SingleObject.GetSingle().AddGameObject(new PlaneEnemy(r.Next(0, this.Width), -400, r.Next(0, 2)));
            }
            //不应该每次都出现最大的敌人飞机，应该有一定的几率出现
            if(r.Next(0,100)> 80)
            {
                //百分之二十的几率出现大飞机
                SingleObject.GetSingle().AddGameObject(new PlaneEnemy(r.Next(0, this.Width), -400, 2));
            }
        }


        /// <summary>
        /// 绘制背景到窗体
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void Form1_Paint(object sender, PaintEventArgs e)
        {
            //当窗体被重新绘制的时候会执行这个控件
            //窗体重新绘制的时候，就绘制自己的背景
            //拿到单例类对象，调用他的Draw函数,通过e传递进来
            SingleObject.GetSingle().Draw(e.Graphics);

            //绘制玩家的得分
            string score = SingleObject.GetSingle().Score.ToString();
            e.Graphics.DrawString(score, new Font("宋体", 20, FontStyle.Bold), Brushes.Red, new Point(0, 0));
        }

        /// <summary>
        /// 让窗体不停的重绘
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void timerBG_Tick(object sender, EventArgs e)
        {
            //每50毫秒让窗体发生重绘事件
            this.Invalidate();//不停的重绘背景
            //不停的绘制完成之后，但是绘制的背景在闪烁，需要解决闪烁的问题

            //不停的判断敌人飞机的数量
            int conut = SingleObject.GetSingle().listPlaneEnemy.Count;
            if (conut <= 1)
            {
                //再次对飞机初始化
                InitialPlaneEnemy();
            }

            //不停进行碰撞检测
            SingleObject.GetSingle().Collision();

        }

        /// <summary>
        /// 解决背景闪烁问题
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void Form1_Load(object sender, EventArgs e)
        {
            //在窗体加载的时候解决窗体的闪烁问题
            //将图像绘制到缓冲区，以减少闪烁次数
            this.SetStyle(ControlStyles.OptimizedDoubleBuffer | ControlStyles.ResizeRedraw | ControlStyles.AllPaintingInWmPaint, true);
        }

        private void Form1_MouseMove(object sender, MouseEventArgs e)
        {
            //当鼠标在窗体移动的时候会触发这个事件，让飞机跟着鼠标的移动而移动
            //通过参数e可以得到鼠标的坐标，把鼠标坐标赋值给玩家飞机坐标即可
            SingleObject.GetSingle().PH.MouseMove(e);

        }

        private void Form1_MouseDown(object sender, MouseEventArgs e)
        {
            //判断玩家是否在窗体按下了鼠标左键
            //按下左键，则调用玩家飞机开炮的方法
            SingleObject.GetSingle().PH.Fire();

        }
    }
}

```

##### GameObject.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace 飞机大战_2020
{

    /// <summary>
    /// 方向
    /// </summary>
    enum Direction // 枚举类型
    {
        Up,
        Down,
        Left,
        Right
    }

    /// <summary>
    /// 所有游戏对象的父类，封装所有子类所共有的成员
    /// </summary>
    abstract class GameObject  //包含抽象成员的类必须也是抽象类
    {
        #region 横纵坐标，高度，宽度，速度，方向，生命值
        public int X //横坐标
        {
            get;
            set;
        }

        public int Y //纵坐标
        {
            get;
            set;
        }

        public int Heigth //高度
        {
            get;
            set;
        }

        public int Width //宽度
        {
            get;
            set;
        }

        public int Speed //速度
        {
            get;
            set;
        }

        public int Life //生命值
        {
            get;
            set;
        }

        public Direction Dir //方向
        {
            get;
            set;
        }
        #endregion

        /// <summary>
        /// 构造函数
        /// </summary>
        /// <param name="x"></param>
        /// <param name="y"></param>
        /// <param name="width"></param>
        /// <param name="heigth"></param>
        /// <param name="speed"></param>
        /// <param name="life"></param>
        /// <param name="dir"></param>
        public GameObject(int x,int y,int width,int heigth,int speed,int life,Direction dir)//构造函数
        {
            this.X = x;
            this.Y = y;
            this.Width = width;
            this.Heigth = heigth;
            this.Speed = speed;
            this.Life = life;
            this.Dir = dir;
        }

        /// <summary>
        /// 构造函数重载，用于Boom函数的构造
        /// </summary>
        /// <param name="x"></param>
        /// <param name="y"></param>
        public GameObject(int x,int y)
        {
            this.X = x;
            this.Y = y;
        }

        //每个游戏对象在GDI+对象绘制自己到窗体的时候绘制的方式不一样。
        //所以我们需要在父类中提供一个绘制对象的抽象函数。

        /// <summary>
        /// 绘制抽象函数，用于绘制对象到窗体
        /// </summary>
        /// <param name="g"></param>
        public abstract void Draw(Graphics g);

        //提供一个碰撞检测的方法，这里返回图片的矩形，判断图片边缘是否重叠，以此来写碰撞检测函数Collision()，在SingleObject里实现

        /// <summary>
        /// 用于 碰撞检测
        /// </summary>
        /// <returns></returns>
        public Rectangle GetRectangle()
        {
            return new Rectangle(this.X, this.Y, this.Heigth, this.Width);
        }

        //需要一个对象移动的函数，子类的移动的方式不一样，所以写成虚拟方法
      
        /// <summary>
        /// 移动的虚拟方法，每一个子类移动方式不一样的自己重写
        /// </summary>
        public virtual void Move()
        {
            //根据游戏对象当前的方向进行移动       
            switch (this.Dir)
            {
                //窗体的左上角为坐标的00原点
                case Direction.Up:
                    this.Y -= this.Speed; //应该是减小时间*速度，时间等会解决
                    break;
                case Direction.Down:
                    this.Y += this.Speed;
                    break;
                case Direction.Left:
                    this.X -= this.Speed;
                    break;
                case Direction.Right:
                    this.X = +this.Speed;
                    break;
            }

            //移动完成之后要判断游戏对象是否超出了窗体边框
            //边框宽480，长850，根据背景图片的大小而定

            //每个对象移动方式不一样，所以判断超出的方式也不一样
            //这里主类写成玩家飞机的，敌人飞机需要重写这个方法

            if (this.X <= 0)
            {
                this.X = 0;
            }
            if (this.X >= 400)
            {
                this.X = 400;
            }
            if (this.Y <= 0)
            {
                this.Y = 0;
            }
            if (this.Y >= 700)
            {
                this.Y = 700;
            }

        }


    }
}
```

##### BackGround.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using 飞机大战_2020.Properties;

namespace 飞机大战_2020
{
    // 背景类
    class BackGround : GameObject
    {
        //首先应该导入背景图片，背景图片需要绘制到窗体上
        private static Image imgBG = Resources.background3;//背景图片,这里的图片直接是文件夹里的文件，后缀没显示

        //写构造函数去调用父类的构造函数
        public BackGround(int x,int y,int speed) : base(x,y,imgBG.Width, imgBG.Height, speed, 0, Direction.Down)
        { }

        //重写Draw函数
        public override void Draw(Graphics g)
        {
            this.Y += this.Speed;
            if (this.Y==0)
            {
                this.Y = -1050;
            }
            //坐标改变完成之后，将背景不停的绘制到窗体中
            g.DrawImage(imgBG, this.X, this.Y);
            //不停绘制的功能在窗体的Timer里实现
        }
    }
}
```

##### PlaneFather.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;  //使用图片
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace 飞机大战_2020
{
    /// <summary>
    /// 所有飞机的父类 抽象类
    /// </summary>
    abstract class PlaneFather : GameObject 
    {
        //声明一个变量，用于存储不同类型飞机的图片
        private Image imgPlane;

        //构造函数调用GameObject构造函数
        public PlaneFather(int x,int y,Image img,int speed,int life,Direction dir):base(x,y,img.Width,img.Height,speed,life,dir)
        {
            this.imgPlane = img;
        }

        //玩家飞机和敌人飞机都会发射子弹
        public abstract void Fire();  //具体的实施不一样，所以写成抽象函数

        //玩家飞机和敌人飞机都会死亡
        public abstract void IsOver();//判断死亡的函数

    }
    
}
```

##### PlaneHero.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using 飞机大战_2020.Properties;

namespace 飞机大战_2020
{
    //玩家飞机类
    class PlaneHero : PlaneFather 
    {
        //导入玩家飞机的图片，保存到图片变量中
        private static Image imgPlane = Resources.me1;//导入玩家飞机的图片

        //调用PlaneFather的构造函数
        public PlaneHero(int x, int y, int speed, int life, Direction dir) : base(x, y, imgPlane, speed, life, dir)
        { }

        //玩家飞机需要重写GameObject中的抽象函数Draw()函数，将自己绘制到窗体上
        public override void Draw(Graphics g)
        {
            g.DrawImage(imgPlane, this.X, this.Y,this.Width/2,this.Heigth/2);
        }

        //让玩家飞机跟着鼠标移动，这个函数需要借助参数e来得到鼠标的坐标
        public void MouseMove(MouseEventArgs e)
        {
            //-27 没有特殊意义，只是为了让鼠标停在玩家飞机的中间
            this.X = e.X - 27;
            this.Y = e.Y - 27;     
        }

        //重写玩家飞机开炮的函数
        public override void Fire()
        {
            //初始化玩家的子弹到游戏中
            SingleObject.GetSingle().AddGameObject(new HeroZiDan(this, 18, 1));//谁，速度，威力

        }

        //玩家飞机死亡的函数
        public override void IsOver()
        {
            //添加爆炸效果
            SingleObject.GetSingle().AddGameObject(new HeroBoom(this.X,this.Y));

            //死亡触发---未写
        }

    }

}
```

##### PlaneEnemy.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using 飞机大战_2020.Properties;

namespace 飞机大战_2020
{
    // 敌人飞机类
    class PlaneEnemy : PlaneFather
    {
        //导入敌人飞机的图片，保存到图片变量中
        private static Image img1 = Resources.enemy1;//小飞机
        private static Image img2 = Resources.enemy2;//中飞机
        private static Image img3 = Resources.enemy3;//大飞机

        static Random r = new Random();//生成一个随机值，用于设计敌人飞机运动轨迹
   
        //三种飞机不一样，大小，生命，速度都不一样，所以要标识当前飞机是哪一架
        //设一个EnmeyType 0--表示小飞机  1--表示中飞机  2--表示大飞机
        public int EnemyType
        {
            get;
            set;
        }

        //根据飞机类型返回图片
        public static Image GetImage(int type)
        {
            switch (type)
            {
                case 0:
                    return img1;
                case 1:
                    return img2;
                case 2:
                    return img3;       
            }
            return null;
        }

        //根据飞机的类型返回生命值
        public static int GetLife(int type)
        {
            switch (type)
            {
                case 0:
                    return 1;
                case 1:
                    return 2;
                case 2:
                    return 3;
            }
            return 0;
        }

        //根据飞机类型返回飞机速度
        public static int GetSpeed(int type)
        {
            switch (type)
            {
                case 0:
                    return 5;
                case 1:
                    return 6;
                case 2:
                    return 7;
            }
            return 0;
        }

        //构造函数，调用PlaneFather的构造函数
        public PlaneEnemy(int x,int y,int type):base(x,y,GetImage(type),GetSpeed(type),GetLife(type),Direction.Down)
        {
            this.EnemyType = type;
        }

        //敌人飞机需要重写GameObject中的抽象函数Draw(),将自己绘制到窗体上
        public override void Draw(Graphics g)
        {
            //随着敌人飞机绘制到窗体，就让他开始移动
            this.Move();
            //根据不同飞机类型绘制不同的飞机
            switch (this.EnemyType)
            {
                case 0:
                    g.DrawImage(img1, this.X, this.Y);
                    break;
                case 1:
                    g.DrawImage(img2, this.X, this.Y);
                    break;
                case 2:
                    g.DrawImage(img3, this.X, this.Y);
                    break;
            }

        }

        //重写Move函数，敌人飞机需要移动出窗体
        public override void Move()
        {
            switch (this.Dir)
            {
                case Direction.Up:
                    this.Y -= this.Speed; //应该是减小时间*速度，时间等会解决
                    break;
                case Direction.Down:
                    this.Y += this.Speed;
                    break;
                case Direction.Left:
                    this.X -= this.Speed;
                    break;
                case Direction.Right:
                    this.X = +this.Speed;
                    break;
            }

            if (this.X <= 0)
            {
                this.X = 0;
            }
            if (this.X >= 400)
            {
                this.X = 400;
            }
            if (this.Y <= 0)
            {
                this.Y = 0;
            }
            if (this.Y >= 700)
            {
                this.Y = 1000;//到达窗体底端，离开窗体
                //同时当敌人飞机离开窗体的时候，需要销毁敌人飞机
                SingleObject.GetSingle().RemoveGameObject(this);
            }

            #region 设置敌人飞机活动轨迹
            if (this.EnemyType == 0 && this.Y >=100 )//小飞机
            {
                if(this.X >=0 && this.X <= 220)
                {
                    //表示小飞机在窗体左侧，我们让他往右偏移一个随机值
                    this.X += r.Next(0, 100);
                }
                else //在窗体的右侧，我们让他往左偏移一个随机值
                {
                    this.X -= r.Next(0, 100);
                }
            }
            else if(this.EnemyType == 1 && this.Y >= 200)//中飞机
            {
                if (this.X >= 0 && this.X <= 250)
                {
                    this.X += r.Next(0, 50);
                }
                else 
                {
                    this.X -= r.Next(0, 50);
                }
            }
            else//大飞机只是加速
            {
                this.Speed += 1;
            }
            #endregion

            //百分之五的几率发射子弹
            if (r.Next(0, 100) > 95)
            {
                Fire();
            }

        }

        //重写死亡函数,判断是否死亡
        public override void IsOver()
        {
            if (this.Life == 0)
            {
                //敌机死亡 应该从游戏中移除
                SingleObject.GetSingle().RemoveGameObject(this);

                //播放敌人爆炸的图片
                SingleObject.GetSingle().AddGameObject(new EnemyBoom(this.X, this.Y,EnemyType));
                
                //敌人发生了爆炸，给玩家加分，根据敌机不同类型加不同的分数
                switch (this.EnemyType)
                {
                    case 0:
                        //需要获得单例中玩家分数的属性
                        SingleObject.GetSingle().Score += 100;
                        break;
                    case 1:
                        SingleObject.GetSingle().Score += 200;
                        break;
                    case 2:
                        SingleObject.GetSingle().Score += 300;
                        break;

                }
               
            }
        }

        //重写开火函数
        public override void Fire()
        {
            SingleObject.GetSingle().AddGameObject(new EnemyZiDan(this,25,1));
        }

    }
}
```

##### ZiDan.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace 飞机大战_2020
{
    //子弹的父类
    class ZiDan : GameObject
    {
        //存储子弹图片
        public Image imgZiDan;

        //记录子弹的威力
        public int Power
        {
            get;
            set;
        }

        //2020.4.16改
        //子弹的发送者，图片，速度，威力，横坐标x，纵坐标y
        public ZiDan(PlaneFather pf, Image img, int speed, int power, int x, int y) : base(x, y, img.Width, img.Height, speed, 0, pf.Dir)
        {
            this.imgZiDan = img;
            this.Power = power;
        }

        //绘制子弹到窗体
        public override void Draw(Graphics g)
        {
            this.Move();
         // g.DrawImage(imgZiDan, this.X, this.Y);
            g.DrawImage(imgZiDan, this.X, this.Y,this.Width,this.Heigth);//可重载设计子弹的大小
        }

        //之前的Move函数当移动到了窗体边缘的时候是停在窗体边缘，而不是射出去，这里做修改
        public override void Move()
        {
            //根据游戏对象当前的方向进行移动       
            switch (this.Dir)
            {
                //窗体的左上角为坐标的00原点
                case Direction.Up:
                    this.Y -= this.Speed; //应该是减小时间*速度，时间等会解决
                    break;
                case Direction.Down:
                    this.Y += this.Speed;
                    break;
            }
            //子弹发出后，控制一下子弹的坐标
            if(this.Y <= 0)
            {
                this.Y = -100;
                //在游戏中移除子弹对象
            }
            if(this.Y >= 780)
            {
                this.Y = 1000;
            }
        }
    }
}
```

##### HeroZiDan.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using 飞机大战_2020.Properties;

namespace 飞机大战_2020
{
    class HeroZiDan : ZiDan
    {
        private static Image imgHero = Resources.bullet1;

        //4.16改
        //pf.X+pf.Width/2-27, pf.Y 中的 /2-27 数值自己调，让飞机从中间发射子弹
        public HeroZiDan(PlaneFather pf, int speed, int power) : base(pf, imgHero, speed, power, pf.X+pf.Width/2-27, pf.Y)
        { }

    }
}
```

##### EnemyZiDan.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using 飞机大战_2020.Properties;

namespace 飞机大战_2020
{
    class EnemyZiDan : ZiDan
    {
        private static Image imgEnemy = Resources.bullet2;

        //pf.X + 10 + pf.Width/2  这里的 +10 是调整飞机中间发射子弹
        public EnemyZiDan(PlaneFather pf, int speed, int power) : base(pf, imgEnemy, speed, power, pf.X + 10 + pf.Width/2, pf.Y+pf.Heigth)
        { }

    }
}
```

##### Boom.cs

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace 飞机大战_2020
{
    // 飞机爆炸函数
    abstract class Boom : GameObject
    {
        //只需要调用父类的构造函数
        //需要知道爆炸的坐标，然后播放爆炸图片
        public Boom(int x,int y) : base(x, y) { }
    }
}
```

##### HeroBoom.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using 飞机大战_2020.Properties;

namespace 飞机大战_2020
{
    class HeroBoom : Boom
    {
        //存储玩家飞机爆炸图片
        private Image[] imgs =  
        {
            Resources.me_destroy_1,
            Resources.me_destroy_2,
            Resources.me_destroy_3,
            Resources.me_destroy_4
        };

        //构造函数调用Boom的构造函数
        public HeroBoom(int x,int y) : base(x, y) { }

        //重写绘制自己到窗体的函数Draw()
        public override void Draw(Graphics g)
        {
            for (int i = 0; i < imgs.Length; i++)
            {
                g.DrawImage(imgs[i], this.X, this.Y,imgs[i].Width/2,imgs[i].Height/2);
            }
            //绘制完成后将爆炸的图片移除
            SingleObject.GetSingle().RemoveGameObject(this);
        }

    }
}
```

##### EnemyBoom.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using 飞机大战_2020.Properties;

namespace 飞机大战_2020
{
    class EnemyBoom : Boom
    {
        //导入每种飞机爆炸时候的图片
        private Image[] imgs1 =
        {
            Resources.enemy1_down1,
            Resources.enemy1_down2,
            Resources.enemy1_down3,
            Resources.enemy1_down4
        };

        private Image[] imgs2 =
        {
            Resources.enemy2_down1,
            Resources.enemy2_down2,
            Resources.enemy2_down3,
            Resources.enemy2_down4
        };

        private Image[] imgs3 =
        {
            Resources.enemy3_down1,
            Resources.enemy3_down2,
            Resources.enemy3_down3,
            Resources.enemy3_down4,
            Resources.enemy3_down5,
            Resources.enemy3_down6
        };

        //爆炸的时候需要知道爆炸是哪一架飞机
        //根据敌人飞机的类型类播放对应的爆炸图片

        public int Type
        {
            get;
            set;
        }

        public EnemyBoom(int x,int y,int type) : base(x, y)
        {
            this.Type = type;
        }

        public override void Draw(Graphics g)
        {
            //将爆炸图片绘制到窗体的时候，需要当前飞机的类型类绘制
            switch (this.Type)
            {
                case 0:
                    for (int i = 0; i < imgs1.Length ; i++)
                    {
                        g.DrawImage(imgs1[i], this.X, this.Y);
                    }
                    break;
                case 1:
                    for (int i = 0; i < imgs2.Length; i++)
                    {
                        g.DrawImage(imgs2[i], this.X, this.Y);
                    }
                    break;
                case 2:
                    for (int i = 0; i < imgs3.Length; i++)
                    {
                        g.DrawImage(imgs3[i], this.X, this.Y);
                    }
                    break;
            }

            //播放完成之后要移除爆炸图片
            SingleObject.GetSingle().RemoveGameObject(this);

        }
    }
}
```

##### SingleObject.cs

```
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace 飞机大战_2020
{
    // 单例类负责所用对象和窗体的交互
    class SingleObject
    {
        //单例类的设计模式
        //1、构造函数私有化
        public SingleObject()
        { }

        //2、声明全局唯一的对象
        private static SingleObject single = null;

        //3、由于创建不了对象，所以提供一个静态函数用于返回一个唯一的对象
        public static SingleObject GetSingle()
        {
            if(single == null)
            {
                single = new SingleObject();
            }
            return single;
        }

        //存储的背景---游戏中唯一的对象
        public BackGround BG
        {
            get;
            set;
        }

        //存储的玩家飞机---游戏中唯一的对象
        public PlaneHero PH
        {
            get;
            set;
        }

        //声明一个集合对象用来 存储玩家子弹对象
        List<HeroZiDan> listHearoZiDan = new List<HeroZiDan>();

        //声明一个集合对象用来 存储敌人子弹对象
        List<EnemyZiDan> listEnemyZiDan = new List<EnemyZiDan>();

        //声明一个集合对象来 存储敌人飞机对象
         public List<PlaneEnemy> listPlaneEnemy = new List<PlaneEnemy>(); //之所以公开，是为了在timer中实时监测还有几架飞机没有销毁

        //声明一个集合对象来 存储敌人飞机爆炸的对象
        List<EnemyBoom> listEnemyBoom = new List<EnemyBoom>();

        //声明一个集合对象来 存储玩家飞机爆炸的对象
        List<HeroBoom> listHeroBoom = new List<HeroBoom>();


        //写一个函数，将创建的对象添加到窗体中
        public void AddGameObject(GameObject go)//由于不知道对象的具体类型，所以传入父类
        {
            if(go is BackGround)//如果当前添加的对象是背景
            {
                this.BG = go as BackGround;//go转成背景赋值给当前的属性
            }
            else if (go is PlaneHero)
            {
                this.PH = go as PlaneHero;
            }
            else if (go is PlaneEnemy)
            {
                listPlaneEnemy.Add(go as PlaneEnemy);
            }
            else if (go is HeroZiDan)
            {
                listHearoZiDan.Add(go as HeroZiDan);
            }
            else if (go is EnemyZiDan)
            {
                listEnemyZiDan.Add(go as EnemyZiDan);
            }
            else if (go is HeroBoom)
            {
                listHeroBoom.Add(go as HeroBoom);
            }
            else if(go is EnemyBoom)
            {
                listEnemyBoom.Add(go as EnemyBoom);
            }


        }

        //写一个函数，将创建的对象从窗体中移除
        public void RemoveGameObject(GameObject go)
        {
            //移除玩家飞机的子弹
            if (go is HeroZiDan)
            {
                listHearoZiDan.Remove(go as HeroZiDan);
            }
            //移除敌人飞机
            else if (go is PlaneEnemy)
            {
                listPlaneEnemy.Remove(go as PlaneEnemy);
            }
            //移除敌人飞机爆炸的图片
            else if (go is EnemyBoom)
            {
                listEnemyBoom.Remove(go as EnemyBoom);
            }
            //移除玩家飞机爆炸的图片
            else if (go is HeroBoom)
            {
                listHeroBoom.Remove(go as HeroBoom);
            }
            //移除敌人飞机的子弹
            else if(go is EnemyZiDan)
            {
                listEnemyZiDan.Remove(go as EnemyZiDan);
            }
            //移除玩家飞机图片
        }

        //这里的Draw函数只是调用其他类本身的Draw函数
        public void Draw(Graphics g)
        {
            this.BG.Draw(g);//向窗体中绘制背景[调用BG的Draw函数绘制背景]
            this.PH.Draw(g);//向窗体中绘制玩家飞机[调用PH的Draw函数绘制玩家飞机]

            //绘制玩家子弹
            for (int i = 0; i < listHearoZiDan.Count; i++)
            {
                listHearoZiDan[i].Draw(g);
            }

            //绘制敌人飞机[三种]
            for (int i = 0; i < listPlaneEnemy.Count; i++)
            {
                listPlaneEnemy[i].Draw(g);
            }

            //绘制敌人飞机爆炸图片
            for (int i = 0; i < listEnemyBoom.Count; i++)
            {
                listEnemyBoom[i].Draw(g);
            }

            //绘制玩家飞机爆炸的图片
            for (int i = 0; i < listHeroBoom.Count; i++)
            {
                listHeroBoom[i].Draw(g);
            }

            //绘制敌人子弹到窗体
            for (int i = 0; i < listEnemyZiDan.Count; i++)
            {
                listEnemyZiDan[i].Draw(g);
            }

        }

        //声明一个属性，用来记分
        public int Score
        {
            get;
            set;
        }

        //碰撞检测函数
        public void Collision()
        {
            #region 判断玩家子弹是否击中敌人飞机
            for (int i = 0; i < listHearoZiDan.Count; i++)//循环玩家子弹
            {
                for (int j = 0; j < listPlaneEnemy.Count; j++)//循环敌人飞机
                {
                    if (listHearoZiDan[i].GetRectangle().IntersectsWith(listPlaneEnemy[j].GetRectangle()))
                    {
                        //如果条件成立则说明发生了碰撞。玩家子弹打中敌人飞机
                        //打中之后敌人的生命值减小 生命值减去子弹威力
                        listPlaneEnemy[j].Life -= listHearoZiDan[i].Power;

                        //生命值减小后判断敌人是否死亡
                        listPlaneEnemy[j].IsOver();

                        //玩家子弹打中后，应该被销毁
                        listHearoZiDan.Remove(listHearoZiDan[i]);//从子弹的集合中去除
                        break;
                    }
                }
            }
            #endregion

            #region 判断敌人子弹是否击中玩家飞机
            for (int i = 0; i < listEnemyZiDan.Count; i++) //遍历敌人子弹
            {
                if (listEnemyZiDan[i].GetRectangle().IntersectsWith(this.PH.GetRectangle()))
                {
                    //满足条件就意味着敌人打中了玩家飞机
                    this.PH.IsOver();
                    break;
                }
            }
            #endregion

            #region 判断玩家飞机是否和敌机飞机相撞
            for (int i = 0; i < listPlaneEnemy.Count; i++)
            {
                if (listPlaneEnemy[i].GetRectangle().IntersectsWith(this.PH.GetRectangle()))
                {
                    //满足条件就意味着玩家飞机和敌机相撞
                    listPlaneEnemy[i].Life = 0;//敌机直接死亡
                    listPlaneEnemy[i].IsOver();
                    break;
                }
            }
            #endregion

            #region 判断玩家子弹是否和敌人子弹相撞
            for (int i = 0; i < listHearoZiDan.Count; i++)
            {
                for (int j = 0; j < listEnemyZiDan.Count; j++)
                {
                    if (listHearoZiDan[i].GetRectangle().IntersectsWith(listEnemyZiDan[j].GetRectangle()))
                    {
                        //满足条件则玩家和敌人子弹移除
                        listHearoZiDan.Remove(listHearoZiDan[i]);
                        listEnemyZiDan.Remove(listEnemyZiDan[j]);
                        break;
                    }
                }
            }

            #endregion

        }
    }
}
```

#### 小结

该代码使用vs2019编译工具，.Net平台，借助winform实现界面。写出完整代码参考了B站上很多老师的课程，在这里致谢各位老师，代码后续还有关于socket的部分还需要完善，后面有时间会继续做下去。
 by 久违 2020.4.15