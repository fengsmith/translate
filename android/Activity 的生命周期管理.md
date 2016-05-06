Activity 的生命周期管理.md
在桌面上点击了应用图标之后发生的变化：
  ● 会调用 main Activity 的 onCreate() 方法
  ● 然后再调用 onStart() 方法
  ● 然后再调用 onResume() 方法
锁屏之后会调用的方法：
  ● 会调用 onPause() 方法
  ● 然后调用 onStop() 方法
解锁屏幕之后会调用的方法：
  ● 会调用 onRestart() 方法
  ● 然后调用 onStart() 方法
  ● 然后调用 onResume() 方法
以上是只有一个 Activity 的情形
下面的情形中有两个 Activity ，点击了 main Activity 上的按钮之后会启动一个新的 Activity ，
我们把由 main Activity 启动的那个 Activity 称之为 display Activity 。
下面是两个 Activity 交互下的 Activity 生命周期，
前提，main Activity 是处于 resumed 状态，在该状态下点击了一个按钮，会启动一个 display Activity ：
  ● 会调用 main Activity 的 onPause() 方法
  ● 然后调用 display Activity 的 onCreate() 方法
  ● 然后调用 display Activity 的 onStart() 方法
  ● 然后调用 display Activity 的 onResume() 方法
  ● 最后会调用 main Activity 的 onStop() 方法
在 display Activity 中点击了后退键之后发生的事件：
  ● 会调用 display Activity 的 onPause() 方法
  ● 然后调用 main Activity 的 onRestart() 方法
  ● 然后调用 main Activity 的 onStart() 方法
  ● 然后调用 main Activity 的 onResume() 方法
  ● 接着会调用 display Activity 的 onStop() 方法
  ● 最后会调用 display Activity 的 onDestroy() 方法
在 main Activity 界面中点击后退按钮后发生的事件：
  ● 会调用 main Activity 的 onPause() 方法
  ● 然后调用 main Activity 的 onStop() 方法
  ● 最后调用 main Activity 的 onDestroy() 方法
在 main Activity 界面中直接点 home 键后发生的事件：
  ● 会调用 main Activity 的 onPause() 方法
  ● 然后调用 main Activity 的 onStop() 方法
在 main Activity 界面中直接点击 home 键后再在桌面上重新点击该应用图标后发生的事件：
  ● 会调用 main Activity 的 onRestart() 方法
  ● 然后调用 main Activity 的 onStart() 方法
  ● 然后调用 main Activity 的 onResume() 方法
杀死应用后发生的事件：
  ● 调用 call stack 上的所有的 Activity 的 onDestroy() 事件
当前 Activity 是 display Activity ，然后点击下拉通知菜单并左右滑动到常用设置时并不会调用任何事件，但点击下拉通知菜单并向右滑动到常用设置页面，点击设置图标会调用的事件：
  ● 会调用 display() 的 onPause() 方法
  ● 然后调用 display() 的 onStop() 方法