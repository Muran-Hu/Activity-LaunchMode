# Activity-LaunchMode
Activity 四种启动模式详解
## 1. standard
#### 这是 Activity 的默认启动模式，每次激活 Activity 的时候都会创建一个新的 Activity 实例，并放入任务栈中。
![示例图片](https://github.com/Muran-Hu/Activity-LaunchMode_standard/blob/master/standard.png)

## 2. singleTop
#### 如果在任务的栈顶正好存有该 Activity 的实例，则会通过调用 onNewIntent() 方法进行重用，否则就会同 standard 模式一样，创建新的实例并放入栈顶。即便栈中已经存在了该 Activity 的实例，也会创建新的实例，即：A -> B ->A，此时栈内为 A -> B -> A，但 A -> B ->B ，此时栈内为 A -> B。一句话概述就是：当且仅当启动的 Activity 和上一个 Activity 一致的时候才会通过调用 onNewIntent() 方法重用 Activity 。
![示例图片](https://github.com/Muran-Hu/Activity-LaunchMode_standard/blob/master/singleTop.png)

## 3. singleTask
#### 这个 launchMode专门用于解决上面 singleTop 的另外一种情况，只要栈中已经存在了该 Activity 的实例，就会直接调用 onNewIntent() 方法来实现重用实例。重用时，直接让该 Activity 的实例回到栈顶，并且移除之前它上面的所有 Activity 实例。如果栈中不存在这样的实例，则和 standard 模式相同。即： A ->B -> C -> D -> B，此时栈内变成了  A -> B。而 A -> B -> C，栈内还是 A -> B -> C。
![示例图片](https://github.com/Muran-Hu/Activity-LaunchMode/blob/master/singleTask.png)

## 4. singleInstance
#### 在一个新栈中创建该 Activity 的实例，并让多个应用共享该栈中的该 Activity 实例。一旦该模式的 Activity 实例已经存在于某个栈中，任何应用再激活该 Activity 时都会重用该栈中的实例，是的，依然是调用 onNewIntent() 方法。其效果相当于多个应用共享一个应用，不管是谁激活，该 Activity 都会进入同一个应用中。但值得引起注意的是：singleInstance 不要用于中间页面，如果用户中间页面，跳转会出现很难受的问题。
![示例图片](https://github.com/Muran-Hu/Activity-LaunchMode/blob/master/singleInstance.png)
