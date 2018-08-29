# Slog53_Unity3D之功能脚本_FindOtherGameObjects_找到场景内除自己外的其他GameObject

* ArthurSlog
* SLog-53
* Year·1

* Guangzhou·China
* Aug 29th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

职业、技术、机遇、权谋、人脉  还有一个 叫 时间

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [UnityEngine.SceneManagement](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.html)

* [Scene](https://docs.unity3d.com/ScriptReference/SceneManagement.Scene.html)

* [GameObject](https://docs.unity3d.com/ScriptReference/GameObject.html)

### 开始编码

* 更新后的完整代码：

unity3d_script_c#/FindOtherGameobjects.cs
``` c#
/// <summary>
/// 2018.8.29
/// Function: Find other gameobjects.
///
/// Unity3D_2017.3.1f1
///
/// README: Please mount a emptyGameObject, then add a button and 
/// the button add a clieck event, drag the emptyGameObject
/// to the button's click's event
/// </summary>

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.AI;
using UnityEngine.SceneManagement;

public class FindOtherGameobjects : MonoBehaviour {

	Scene current_scene;
	GameObject[] objs;

	void Start()
	{
		current_scene = SceneManager.GetActiveScene ();
	}

	public void FindOtherobj()
	{
		if(current_scene.IsValid())
		{
			objs = current_scene.GetRootGameObjects ();

			foreach (GameObject obj in objs)
			{
				if (obj.name != this.name)
				{
                    Debug.Log ("Active scene have '" + obj.name + "'.");
				}
			}
		}
	}
}
```

* 首先声明一个 Scene对象，当调用脚本的时候，获取当前 Scene对象

* 再声明一个 GameObject数组 对象 objs，用来存放当前 Scene里 的所有 GameObject

* 遍历所有的 GameObject，加入判断，当 Scene里的 GameObject 的name属性不等于自身的时候，执行指定的逻辑

* 我们在这里的指定逻辑是

unity3d_script_c#/FindOtherGameobjects.cs
``` c#
Debug.Log ("Active scene have '" + obj.name + "'.");
```

* 这样，我们就打印出了除了自身外，其他 GameObject的 name属性了

* 如果要对自身外的其他 GameObject进行一些操作，更新下面的这行代码就行了：

unity3d_script_c#/FindOtherGameobjects.cs
``` c#
Debug.Log ("Active scene have '" + obj.name + "'.");
```

* 至此，我们实现了 unity3d 找到场景内除自己外的其他GameObject 的功能。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
