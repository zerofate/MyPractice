> 背景：newInstance 一开始肯定是一个的，但是为了快速完成需求，为了复用，于是就进行了重载，这样就能用多个 newInstance 来满足了两种场景。一开始，我对于这种用法需要有说不上的违和感，但也说不上哪里不好，而且谷歌也没找到这种用法的弊端，或者说我并没有找到有人这样用。。。但这也不能说不能这样用啊。不过，在看多了这种用法，并且在这种用法的基础下增加了一些代码后，的确发觉这种用法存在很大的问题。

弊端：

+ 两个 newInstance 方法的参数不同，说明他们的实例在使用时肯定有另外一个 newInstance 的依赖，这样会导致该 Fragment 类变得越来越难以维护。
+ newInstance 的参数不同，往往以为着该类的职责有了变化，这样就违反了单一职责原则



改善：首先需要明白产生多个 newInstance 的原因，然后采取适当的方案。细想一下，好像我也总结不出什么来，只能大概说明下自己的看法，增加 newInstance 就是为了引入新的依赖，用于实现新的功能，而之所以重载是为了复用旧的 UI 与 逻辑，在这种情况下，创建一个新的基类应该比重载 newInstance 更好吧。