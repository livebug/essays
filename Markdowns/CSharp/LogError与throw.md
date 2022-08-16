# `LogError` 与 `throw` 的差异

网上的回复：

+ >The throw keyword is specifically intended to throw an exception. If you want to throw an exception then use it and if you don't want to then don't use it. If they aren't using it then obviously they don't want to throw an exception. If they are using Debug.LogError then presumably they only want to log an error while debugging. Logging an error just means writing somewhere that it happened but the app carries on normally otherwise. Throwing an exception means terminating all executing methods until a handler catches it or else crashing the app. Very different behaviours.


+ >Most of the time they are not the same thing. One obvious difference is, when you throw an exception from a method, rest of the method will not be run and exception will be passed to calling method.Exceptions are literally for exceptional cases. It means something has gone wrong. When something goes wrong you might want to correct it and continue running, or simply stop running. I can't know for what purpose you use Exception in your case. But know that LogError will not cause function to quit but throwing Exception will.

大多数时候它们不是一回事。一个明显的区别是，当从方法引发异常时，不会运行方法的其余部分，异常将传递给调用方法。   
特殊情况才会有特殊情况。意思是出事了。当出现错误时，您可能希望纠正它并继续运行，或者干脆停止运行。我不知道在这种情况下使用 Exception 的目的是什么。但要知道，`LogError` 不会导致函数退出，但引发 `Exception` 会。

抛出异常，是为了后续的捕获或者处理

日志报错，只是记录报错，程序还是正常跑