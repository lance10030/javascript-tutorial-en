当我们看下面这个函数里面的代码，差异就很明显了。

如果能够跳出 `try..catch`，表现就不同了。

例如，当 try..catch 里有 return 的时候，finally 代码块会在退出 try..catch 后继续执行，即使是通过 return 语句退出的。它会在再后面的代码执行之前，在 try..catch 执行完之后立即执行。

function f() {
  try {
    alert('start');
*!*
    return "result";
*/!*
  } catch (e) {
    /// ...
  } finally {
    alert('cleanup!');
  }
}

f(); // cleanup!
...或者当有 throw 的时候，如下:

function f() {
  try {
    alert('start');
    throw new Error("an error");
  } catch (e) {
    // ...
    if("can't handle the error") {
*!*
      throw e;
*/!*
    }

  } finally {
    alert('cleanup!')
  }
}

f(); // cleanup!
它保证了 cleanup 的显示，但是如果把这行代码放在 函数 f 之后，那么，它不会执行。
