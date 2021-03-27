#基本工具的使用
   * VSCode及拓展:主要IDE
   * Cmder:终端修改工具,支持git命令,自定义主题,tab分页,同屏多端口
   * rap2:可视化接口管理工具,可以在没有后端数据提供的时候使用随机数据模拟,支持mock.js语法
      * ex: 
         * "mtime": "@datetime",//随机生成日期时间 
         * "score|1-800": 800,//随机生成1-800的数字
         * "rank|1-100":  100,//随机生成1-100的数字
         * "stars|1-5": 5,//随机生成1-5的数字
         * "nickname": "@cname",//随机生成中文名字
   * postman:用于接口测试,可以拦截请求
   * typora:类似于markdownpad 2,md编辑器
   * licecap:屏幕录制
----
#git常用指令
   * git init:将该目录编程Git可以管理的仓库
   * git add xxx.xxx:把文件添加到仓库中
   * git commit -m:把文件提交到仓库,-m后面可以输入本次提交的说明
   * git status:查看仓库当前状态
   * git diff xxx.xxx:查看文件修改的部分
   * git diff --cached:查看暂存区和仓库的差异
   * git log:显示从最近到最远的提交日志
   * git reset --hard HEAD^或者git reset --hard 版本号:回退到上一个版本,HEAD^表示上一个版本,上上一个版本就是HEAD^^,HEAD~100 回滚到100个版本之前
   * git reflog:查看记录的每一次命令
   * git仓库结构
      ![git仓库结构](https://raw.githubusercontent.com/AmazingTsky/PICS/main/%E4%BB%93%E5%BA%93.jpg)
   * git diff HEAD -- readme.txt:查看工作区和版本库里面最新版本的区别
   * git checkout -- file:丢弃工作区的修改,也可以把误删的文件恢复到最新版本
   * git reset HEAD <file>:把暂存区的修改撤销掉,git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。
   * git rm <file>:将文件从版本库中删除,工作区也会删除,添加--cached参数后只会从索引中删除文件,即本地文件还在;当通过rm删除文件后可以通过git reset;git checkout <file>来进行恢复
   * git remote add origingit@git'.com:关联github远程仓库
   * git push:把本地库的内容推送到远程,第一次推送加上 -u参数
   * git remote rm <name>:删除仓库,使用前建议先用git remote -v查看远程库信息
   * git clone:克隆一个本地库
   * git checkout -b:创建并切换,它等价于:git branch dev;git checkout dev;
   * git merge <branch>:用于合并指定分支到当前分支
   * git branch -d <branch>:删除已经合并的分支
   * git branch -D <branch>:在没检查是否合并的情况下直接删除分支
   * git switch -c <branch>:切换到分会,相对合理.可以使用-c，-c从同名的远程分支中自动创建一个新分支（请参阅--guess），或者使用--detach在切换的时候，将工作树从任何分支中分离出来。
   * git log:提交信息,可以添加多种参数
      * 搜索参数为提交的创建者和提交者
         * git log  --author=<pattern>git log --committer=<pattern>
      * 某个日期之后
         * git log --since=<date>
         * git log --after=<date>
      * 某个日期之前
         * git log --until=<date>
         * git log --before=<date>
      * 具体的时间区间
         * git log --since="2018.03.12" --until="2018.03.18"
      * 搜索提交信息
         * git log --grep='喜欢' --oneline
      * 查看某个字符串的变动历史提交
         * git log -S<string>
      * 查看某符合某一个正则表达式内容的变动历史提交
         * git log -G<regex>
      * 查看发生合并冲突的文件
         * git log --merge
      * –graph:选项会绘制一个 ASCII 图像来展示提交历史的分支结构。
      * –decorate:是用来可以显示出指向提交的指针的名字，也就是 HEAD 指针, feature/test等分支名称，还有远程分支，标签等。
   * git merge --no-ff 会让 Git 生成一个新的提交对象(推荐)
   * git stash:保存工作现场
   * git stash apply:恢复,此时stash中内容并不会删除
   * git stash drop:删除
   * git stash pop:恢复的同时把stash也删除了
   * git stash list:查看stash中的内容
   * git cherry-pick 4c805e2:自动提交和4c一样的改动
   * git remote show:查看远程库信息,添加-v可以显示更详细的信息
   * remote name:具体指定一个主机
   * git branch --set-upstream-to <branch-name> origin/<branch-name>:创建本地分支和远程分支的链接
   * git rebase:可以把本地未push的分叉提交历史整理成直线；rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。
   * git tag  <name>:打标签
   * git tag:查看所有标签
   * git show<tgname>:查看标签信息
   * git tag -a xxx -m"xxx" 10ex1s1:-a用于指定标签名,-m添加说明性文字
   * git push:    git push的一般形式为 git push <远程主机名> <本地分支名>  <远程分支名> ，例如 git push origin master：refs/for/master ，即是将本地的master分支推送到远程主机origin上的对应master分支， origin 是远程主机名
      * git push origin master如果远程分支被省略，如上则表示将本地分支推送到与之存在追踪关系的远程分支（通常两者同名），如果该远程分支不存在，则会被新建
      * git push origin :refs/for/master: 如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支，等同于 git push origin --delete master
      * git push origin :refs/tags/v0.9:从远程删除标签(首先要现在本地 git tag -d v0.9删除标签)
      * git push origin: 如果当前分支与远程分支存在追踪关系，则本地分支和远程分支都可以省略，将当前分支推送到origin主机的对应分支
      * git push:　如果当前分支只有一个远程分支，那么主机名都可以省略，形如 git push，可以使用git branch -r ，查看远程的分支名
      * git push Note --delete dev:删除Note远程库的dev分支
      * git branch -d dev:删除dev分支 
   * git restore --staged<file>:可以取消暂存
   * git restore:丢弃工作区的改动
----
#Source Tree:Git可视化
---
#Chrome Devtools
   * Generic
      * copy:复制任何东西
      * store:选中元素:store as global variable存储为全局变量,可以结合copy进行复制
      * Sources下snippets:新建代码片段,右击直接run
      * command:命令行工具ctrl+shift+p打开
   * Elements:
      * 可以通过Ctrl+C直接复制
      * 可以直接拖动标签修改排序,按H可以隐藏元素.
      * 右键元素代码选择Scroll into view可以根据代码找元素
      * 查看效果
      ![查看效果](https://raw.githubusercontent.com/AmazingTsky/PICS/main/%E6%9F%A5%E7%9C%8B%E6%95%88%E6%9E%9C.jpg)
   * 右键元素的代码,此时元素不会被移除,可以打断点
   * monitorEvents($0):监听当前选中元素触发了哪些事件
   * Elements:Event Listenner查看绑定的事件

   * Console
      * $0:当前选中的节点
      ![当前选中的节点](https://raw.githubusercontent.com/AmazingTsky/PICS/main/%E5%BD%93%E5%89%8D%E9%80%89%E4%B8%AD%E8%8A%82%E7%82%B9.jpg)
      * $1:上一个选中的节点
      * $$("div"):所有的div标签,选中某种元素
      * $_:执行上一次表达式的结果
      * console
   * Network
      * 第一个选项可以设置隐藏请求地址,第二个可以隐藏预览
      ![network](https://raw.githubusercontent.com/AmazingTsky/PICS/main/network.jpg)
      * 右键选择reply可以重新发送请求不用刷新
      ![reply](https://raw.githubusercontent.com/AmazingTsky/PICS/main/reply.jpg)
   * Application:可以查看本地存储,cookie等
   * Sources:添加请求,向改地址发送请求时执行断点
---
#React基本用法
   * 定义一个组件:
   ```
   function HelloMessage(props) {
    return <h1>Hello World!</h1>;
   }
   ```
   ```
    class Welcome extends React.Component {
 	 render() {
   		 return <h1>Hello World!</h1>;
  				}
	}
   ```
   * 复合组件
   ```
   function Name(props) {
    return <h1>网站名称：{props.name}</h1>;
	}
	function Url(props) {
    return <h1>网站地址：{props.url}</h1>;
	}
	function Nickname(props) {
    return <h1>网站小名：{props.nickname}</h1>;
	}
	function App() {
    return (
    <div>
        <Name name="菜鸟教程" />
        <Url url="http://www.runoob.com" />
        <Nickname nickname="Runoob" />
    </div>
    );
	}
   ```
   * state和props的区别
      * **state是组件自己管理数据，控制自己的状态，可变**；
      * **props是外部传入的数据参数，不可变**；
      * **没有state的叫做stateless无状态组件，有state的叫做有状态组件**；
      * state应该包括哪些可能被组件的事件处理器改变并处罚用户界面更新的数据,因为组件不能修改本身的prop	
   * props验证:Props 验证使用 propTypes，它可以保证我们的应用组件被正确使用，React.PropTypes 提供很多验证器 (validator) 来验证传入数据是否有效。当向 props 传入无效数据时，JavaScript 控制台会抛出警告。
   ```
   var title = "菜鸟教程";
	// var title = 123;
	class MyTitle extends React.Component {
 	 render() {
   	 return (
      <h1>Hello, {this.props.title}</h1>
    );
  	}
}
 
MyTitle.propTypes = {
  title: PropTypes.string
};
ReactDOM.render(
    <MyTitle title={title} />,
    document.getElementById('example')
);
   ```
   * 更多验证器:
   ```
   MyComponent.propTypes = {
    // 可以声明 prop 为指定的 JS 基本数据类型，默认情况，这些数据是可选的
   optionalArray: React.PropTypes.array,
    optionalBool: React.PropTypes.bool,
    optionalFunc: React.PropTypes.func,
    optionalNumber: React.PropTypes.number,
    optionalObject: React.PropTypes.object,
    optionalString: React.PropTypes.string,
 
    // 可以被渲染的对象 numbers, strings, elements 或 array
    optionalNode: React.PropTypes.node,
 
    //  React 元素
    optionalElement: React.PropTypes.element,
 
    // 用 JS 的 instanceof 操作符声明 prop 为类的实例。
    optionalMessage: React.PropTypes.instanceOf(Message),
 
    // 用 enum 来限制 prop 只接受指定的值。
    optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),
 
    // 可以是多个对象类型中的一个
    optionalUnion: React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
      React.PropTypes.instanceOf(Message)
    ]),
 
    // 指定类型组成的数组
    optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),
 
    // 指定类型的属性构成的对象
    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),
 
    // 特定 shape 参数的对象
    optionalObjectWithShape: React.PropTypes.shape({
      color: React.PropTypes.string,
      fontSize: React.PropTypes.number
    }),
 
    // 任意类型加上 `isRequired` 来使 prop 不可空。
    requiredFunc: React.PropTypes.func.isRequired,
 
    // 不可空的任意类型
    requiredAny: React.PropTypes.any.isRequired,
 
    // 自定义验证器。如果验证失败需要返回一个 Error 对象。不要直接使用 `console.warn` 或抛异常，因为这样 `oneOfType` 会失效。
    customProp: function(props, propName, componentName) {
      if (!/matchme/.test(props[propName])) {
        return new Error('Validation failed!');
      }
    }
  }
}
   ```
-----
#CSS
   * 定位
      * static
      * fixed
      * absolute
      * relative
      * sticky
   * 居中.

   		1. 父元素设置text-align:center,子元素要居中必须是inline元素或者inline-block元素(inline元素没有宽高属性).
   		2. magin:auto:对浮动元素不能达到居中效果
   		3. margin:如果设置为 magin:3 2 1,3控制上,2控制左右,1控制下
   		4. 垂直居中:line-height:(height值)注意border-box,此时CSS分离原则可以起作用
   		5. vertical-align:middle:必须有参照物,可以通过设置伪元素实现.vertical-align可以设置具体数值进行微调.
   * CSS宽高分离:嵌套一层标签，给父元素设置宽度，子元素因为width使用的是默认值auto，所以会自动填满容器,这个时候不用计算宽高就可以让内容自动变化.
		```

   		.box-father {
   		width: 100px;
   		}
   		.box {
   		padding: 20px;
   		 border: 1px solid red;
   		}
   	 	.box {
   		 padding: 20px;
   		width: 60px;            // 通过计算减去40px
   		border: 1px solid red;
   		 }
   		```
   * css使用3D如transform:translate3D(-50%,-50%,0)开启GPU渲染加速.
   * padding:padding使用百分比的时候是基于父元素的宽度设定的.
   * label的for属性:可以通过过用label包裹input实现,和设置label的for和input的id一样的效果,label实现单选效果必须设置同样的name.
   * 伪元素:(双冒号)::before和::after都必须和content属性结合使用,content不能没有,至少为空,伪元素默认为inline,可以自己更改.
   * flex布局(弹性布局,设置display:flex 实现,行内元素也可以通过display:inline-flex实现)
      * 在设置flex布局后,子元素的float、clear和vertical-align属性将失效.
      * ![flex容器](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)
        * 容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

          * flex-direction属性决定主轴的方向（即项目的排列方向）
          * row（默认值）：主轴为水平方向，起点在左端。
          * row-reverse：主轴为水平方向，起点在右端。
          * column：主轴为垂直方向，起点在上沿。
          * column-reverse：主轴为垂直方向，起点在下沿。
          * flex-wrap属性:默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。
          * nowrap（默认）：不换行。
          * wrap：换行，第一行在上方。
          * wrap-reverse：换行，第一行在下方。

          * flex-flow属性:flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
          * justify-content属性:定义了项目在主轴上的对齐方式。
          	* flex-start（默认值）：左对齐
          	* flex-end：右对齐
          	* center： 居中
          	* space-between：两端对齐，项目之间的间隔都相等。
          	* space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
          * align-items属性:定义项目在交叉轴上如何对齐。
          	* flex-start：交叉轴的起点对齐。
          	* flex-end：交叉轴的终点对齐。
          	* center：交叉轴的中点对齐。
          	* baseline: 项目的第一行文字的基线对齐。
          	* stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
          * align-content属性:定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
          	* flex-start：与交叉轴的起点对齐。
          	* flex-end：与交叉轴的终点对齐。
          	* center：与交叉轴的中点对齐。
          	* space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
          	* space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
          	* stretch（默认值）：轴线占满整个交叉轴。
-----
#ES6
		
 						