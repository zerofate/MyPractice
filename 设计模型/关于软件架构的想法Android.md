在开发过程中，随着需求的不断增加、变更，甚至一些接口的变动，都会导致我们的代码变得越来越丑陋。MVC、MVP、MVVM、clean architecture，从我开始学习 Android 到现在，很自然地接触到这几种架构，不过使用得却很少，并且也不够熟悉。但在实际开发过程中，对于这些架构应解决的问题，却越来越有体会，特别是在新公司的项目里看到 MVP 的运用。

MVC 没什么好说的。而对于 MVP 却是越来越有体会。在我看来，架构的运用的最大难点并不在于逻辑与 View 的分离，而是数据的分离，而在公司代码里的 MVP 却没有做到这一点，仅有 VP 而没有 M 的封装。