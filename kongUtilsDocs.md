## 检测手机号码

### JS实现

以下是一个用JS编写的检测手机号码的工具函数：

```javascript
function isPhoneNumber(phoneNumber) {
  const regex = /^1[3-9]\d{9}$/;
  return regex.test(phoneNumber);
}
```

这个函数接受一个字符串参数，即待检测的手机号码。

它使用正则表达式来验证手机号码是否符合规范。

如果手机号码符合规范，则返回true，否则返回false。

正则表达式`/^1[3-9]\d{9}$/`的含义是：

- `/^`表示从字符串的开头开始匹配；
- `1`表示手机号码的第一位必须是数字1；
- `[3-9]`表示手机号码的第二位必须是数字3至9中的任意一个；
- `\d{9}`表示后面必须跟着9个数字；
- `$/`表示匹配到字符串的结尾。

因此，这个正则表达式可以匹配符合规范的11位手机号码。

### TS实现

以下是一个用TypeScript编写的检测手机号码的工具函数：

```typescript
function isPhoneNumber(phoneNumber: string): boolean {
  const regex: RegExp = /^1[3-9]\d{9}$/;
  return regex.test(phoneNumber);
}
```

这个函数与上面的JavaScript版本的函数基本相同，只是在参数和变量声明时添加了类型注解。

参数`phoneNumber`被注解为字符串类型，返回值被注解为布尔类型。

变量`regex`被注解为RegExp类型，这样可以确保只有正则表达式可以赋值给它。

使用TypeScript 我们可以在编译时捕获一些类型错误，从而提高代码的可靠性和可维护性。



## 检测身份证号码

### JS实现

以下是一个用JS编写的检测身份证号码的工具函数：

```javascript
function isIDCard(idCard) {
  const regex = /(^\d{15}$)|(^\d{17}([0-9]|X)$)/;
  if (!regex.test(idCard)) {
    return false;
  }
  const provinceCode = idCard.substring(0, 2);
  if (parseInt(provinceCode) < 11 || parseInt(provinceCode) > 91) {
    return false;
  }
  const year = idCard.substring(6, 10);
  const month = idCard.substring(10, 12);
  const day = idCard.substring(12, 14);
  const date = new Date(year + '-' + month + '-' + day);
  if (date.getFullYear() != parseInt(year) || date.getMonth() + 1 != parseInt(month) || date.getDate() != parseInt(day)) {
    return false;
  }
  let sum = 0;
  const weight = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2];
  const checkCode = ['1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2'];
  for (let i = 0; i < idCard.length - 1; i++) {
    sum += parseInt(idCard.charAt(i)) * weight[i];
  }
  const remainder = sum % 11;
  if (idCard.charAt(idCard.length - 1).toUpperCase() != checkCode[remainder]) {
    return false;
  }
  return true;
}
```

这个函数接受一个字符串参数，即待检测的身份证号码。它使用正则表达式来验证身份证号码是否符合规范。

如果身份证号码符合规范，则进一步检查省份、出生日期和校验码是否正确，如果都正确，则返回true，否则返回false。

正则表达式`/(^\d{15}$)|(^\d{17}([0-9]|X)$)/`的含义是：

- `/^`表示从字符串的开头开始匹配；
- `(^\d{15}$)`表示匹配15位数字的身份证号码；
- `|`表示或者；
- `(^\d{17}([0-9]|X)$)`表示匹配18位数字或17位数字加上一个大写字母X的身份证号码；
- `$/`表示匹配到字符串的结尾。

因此，这个正则表达式可以匹配符合规范的15位和18位身份证号码。

此外，还使用了其他的校验逻辑，包括检查省份代码是否正确、出生日期是否正确以及校验码是否正确。这些校验逻辑可以确保身份证号码的有效性。

### TS实现

以下是一个用TypeScript编写的检测身份证号码的工具函数：

```typescript
function isIDCard(idCard: string): boolean {
  const regex: RegExp = /(^\d{15}$)|(^\d{17}([0-9]|X)$)/;
  if (!regex.test(idCard)) {
    return false;
  }
  const provinceCode: string = idCard.substring(0, 2);
  if (parseInt(provinceCode) < 11 || parseInt(provinceCode) > 91) {
    return false;
  }
  const year: string = idCard.substring(6, 10);
  const month: string = idCard.substring(10, 12);
  const day: string = idCard.substring(12, 14);
  const date: Date = new Date(year + '-' + month + '-' + day);
  if (date.getFullYear() != parseInt(year) || date.getMonth() + 1 != parseInt(month) || date.getDate() != parseInt(day)) {
    return false;
  }
  let sum: number = 0;
  const weight: number[] = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2];
  const checkCode: string[] = ['1', '0', 'X', '9', '8', '7', '6', '5', '4', '3', '2'];
  for (let i: number = 0; i < idCard.length - 1; i++) {
    sum += parseInt(idCard.charAt(i)) * weight[i];
  }
  const remainder: number = sum % 11;
  if (idCard.charAt(idCard.length - 1).toUpperCase() != checkCode[remainder]) {
    return false;
  }
  return true;
}
```

这个函数与上面的JavaScript版本的函数基本相同，只是在参数和变量声明时添加了类型注解。参数`idCard`被注解为字符串类型，返回值被注解为布尔类型。

变量`regex`被注解为RegExp类型，这样可以确保只有正则表达式可以赋值给它。



## 检测银行卡号

### JS实现

以下是一个用JS编写的检测银行卡号的工具函数：

```javascript
function checkBankCardNumber(cardNumber) {
  // 去除空格
  cardNumber = cardNumber.replace(/\s+/g, '');
  // 校验长度和数字
  if (cardNumber.length !== 16 && cardNumber.length !== 19) {
    return false;
  }
  if (/^\d*$/.test(cardNumber) === false) {
    return false;
  }
  // 校验银行卡号
  const lastDigit = parseInt(cardNumber[cardNumber.length - 1], 10);
  const cardNumberWithoutLastDigit = cardNumber.slice(0, -1);
  const reversedDigits = cardNumberWithoutLastDigit.split('').reverse().map(digit => parseInt(digit, 10));
  const doubledDigits = reversedDigits.map((digit, index) => {
    if (index % 2 === 0) {
      return digit;
    } else {
      const doubledDigit = digit * 2;
      return doubledDigit > 9 ? doubledDigit - 9 : doubledDigit;
    }
  });
  const sum = doubledDigits.reduce((acc, digit) => acc + digit, lastDigit);
  return sum % 10 === 0;
}
```

这个函数接受一个字符串参数`cardNumber`，即待检测的银行卡号。它使用一系列校验规则来判断银行卡号是否合法，最终返回一个布尔值。

首先，我们使用正则表达式和`replace()`方法去除银行卡号中的所有空格。然后，我们校验银行卡号的长度和数字。16位银行卡号和19位银行卡号都是合法的，但银行卡号必须是纯数字，不能包含其他字符。

接下来，我们使用Luhn算法来校验银行卡号。Luhn算法是一种校验和算法，用于验证一些识别号码的有效性，例如信用卡号、社会保障号码等。

我们首先将银行卡号最后一位数字取出来，并将其从银行卡号中删除。然后，我们将剩余的银行卡号倒序排列，并将每个数字转换成整数类型。接着，我们将每个偶数位上的数字翻倍，并将其转换成一位数字。最后，我们将所有数字加起来，并加上之前取出的最后一位数字。如果这个和可以被10整除，则银行卡号合法；否则不合法。

注意：这个函数只是一个简单的实现，无法保证100%准确性。在实际应用中，应该使用更加严格和完善的校验规则来确保银行卡号的有效性。

### TS实现

以下是一个用TypeScript实现的检测银行卡号的工具函数：

```typescript
function checkBankCardNumber(cardNumber: string): boolean {
  // 去除空格
  cardNumber = cardNumber.replace(/\s+/g, '');
  // 校验长度和数字
  if (cardNumber.length !== 16 && cardNumber.length !== 19) {
    return false;
  }
  if (/^\d*$/.test(cardNumber) === false) {
    return false;
  }
  // 校验银行卡号
  const lastDigit = parseInt(cardNumber[cardNumber.length - 1], 10);
  const cardNumberWithoutLastDigit = cardNumber.slice(0, -1);
  const reversedDigits = cardNumberWithoutLastDigit.split('').reverse().map(digit => parseInt(digit, 10));
  const doubledDigits = reversedDigits.map((digit, index) => {
    if (index % 2 === 0) {
      return digit;
    } else {
      const doubledDigit = digit * 2;
      return doubledDigit > 9 ? doubledDigit - 9 : doubledDigit;
    }
  });
  const sum = doubledDigits.reduce((acc, digit) => acc + digit, lastDigit);
  return sum % 10 === 0;
}
```

这个函数与上面的JavaScript版本的函数基本相同，只是在参数和返回值声明时添加了类型注解。参数`cardNumber`被注解为字符串类型，返回值被注解为布尔类型。



## 解析URL参数

### JS实现

以下是一个用JS编写的解析url参数的工具函数：

```javascript
function parseUrlParams(url) {
  const params = {};
  const searchParams = new URLSearchParams(url.split('?')[1]);
  for (const [key, value] of searchParams.entries()) {
    params[key] = value;
  }
  return params;
}
```

这个函数接受一个字符串参数，即待解析的url。

它使用`URLSearchParams`对象来解析url中的查询参数，并将其存储在一个对象中返回。

首先，我们创建一个空对象`params`来存储解析后的参数。

然后，我们使用`split()`方法将url字符串分成两部分，即路径和查询参数部分。

我们只需要查询参数部分，因此使用`[1]`获取它。

接下来，我们使用`URLSearchParams`对象来解析查询参数。这个对象提供了许多方法，例如`entries()`方法可以返回一个可迭代对象，其中包含所有的查询参数键值对。我们使用`for...of`循环遍历这个可迭代对象，并将每个键值对存储在`params`对象中。

最后，我们返回`params`对象，其中包含解析后的所有查询参数。

### TS实现

以下是一个用TypeScript实现的解析url参数的工具函数：

```typescript
function parseUrlParams(url: string): Record<string, string> {
  const params: Record<string, string> = {};
  const searchParams = new URLSearchParams(url.split('?')[1]);
  for (const [key, value] of searchParams.entries()) {
    params[key] = value;
  }
  return params;
}
```

这个函数与上面的JavaScript版本的函数基本相同，只是在参数和变量声明时添加了类型注解。

返回值被注解为一个键值对对象，其中键和值都是字符串类型。



## 字符串空格处理

### JS实现

以下是一个用JS编写的字符串空格处理的工具函数，可以处理前后空格和所有空格：

```javascript
function trimAll(str) {
  return str.replace(/\s+/g, '').trim();
}
```

这个函数接受一个字符串参数`str`，即待处理的字符串。

它使用`replace()`方法和正则表达式来删除所有空格，并使用`trim()`方法来删除字符串首尾的空格。

正则表达式`/\s+/g`的含义是：

- `/`表示正则表达式的开始；
- `\s+`表示匹配一个或多个空格字符；
- `/g`表示全局匹配，即匹配所有空格字符。

因此，这个正则表达式可以匹配所有空格字符，包括空格、制表符、换行符等。

最后，我们返回处理后的字符串。如果原始字符串中只有前后空格，则返回去除前后空格后的字符串；如果原始字符串中还包含其他空格，则返回去除所有空格后的字符串。

### TS实现

以下是一个用TypeScript实现的字符串空格处理的工具函数，可以处理前后空格和所有空格：

```typescript
function trimAll(str: string): string {
  return str.replace(/\s+/g, '').trim();
}
```

这个函数与上面的JavaScript版本的函数基本相同，只是在参数和返回值声明时添加了类型注解。

参数`str`被注解为字符串类型，返回值也被注解为字符串类型。



## 防抖

### JS实现

以下是一个可以处理一些复杂场景的防抖函数：

```javascript
function debounce(func, delay, immediate = false) {
  let timeoutId;
  let result;
  let callNow = immediate;
  let debouncedFunction = function(...args) {
    const context = this;
    const later = function() {
      timeoutId = null;
      if (!immediate) {
        result = func.apply(context, args);
      }
    };
    clearTimeout(timeoutId);
    timeoutId = setTimeout(later, delay);
    if (callNow) {
      result = func.apply(context, args);
      callNow = false;
    }
    return result;
  };
  debouncedFunction.cancel = function() {
    clearTimeout(timeoutId);
  };
  return debouncedFunction;
}
```

这个函数接受三个参数：`func`是要执行的函数，`delay`是防抖的时间间隔，单位为毫秒，`immediate`是一个可选的布尔值，表示是否在第一次调用时立即执行函数。

当调用防抖函数返回的新函数时，它会使用`setTimeout()`函数来延迟执行`func`函数。

如果在延迟时间内多次调用新函数，则会清除之前的定时器，并重新设置一个新的定时器，以保证`func`函数在最后一次调用后才会被执行。

如果设置了`immediate`为`true`，则会在第一次调用时立即执行`func`函数，并在延迟时间内忽略后续的调用。

此外，这个函数还提供了一个`cancel()`方法，用于取消尚未执行的定时器。

注意：这个函数只是一个简单的实现，无法处理所有复杂场景。在实际应用中，应该根据具体场景选择更加适合的防抖方案。

### TS实现

以下是一个可以处理一些复杂场景的防抖函数的TypeScript实现：

```typescript
type DebouncedFunction<T extends (...args: any[]) => any> = {
  (...args: Parameters<T>): ReturnType<T> | undefined;
  cancel: () => void;
};

function debounce<T extends (...args: any[]) => any>(func: T, delay: number, immediate = false): DebouncedFunction<T> {
  let timeoutId: ReturnType<typeof setTimeout>;
  let result: ReturnType<T> | undefined;
  let callNow = immediate;
  const debouncedFunction = function(this: unknown, ...args: Parameters<T>): ReturnType<T> | undefined {
    const context = this;
    const later = function() {
      timeoutId = null;
      if (!immediate) {
        result = func.apply(context, args);
      }
    };
    clearTimeout(timeoutId);
    timeoutId = setTimeout(later, delay);
    if (callNow) {
      result = func.apply(context, args);
      callNow = false;
    }
    return result;
  } as DebouncedFunction<T>;
  debouncedFunction.cancel = function() {
    clearTimeout(timeoutId);
  };
  return debouncedFunction;
}
```

这个函数与上面的JavaScript版本的函数基本相同，只是在参数和返回值声明时添加了类型注解，并定义了一个`DebouncedFunction`类型，用于声明防抖函数的类型。

`DebouncedFunction`类型是一个函数类型和一个`cancel()`方法的组合。



## 节流

### JS实现

以下是一个用JS编写的节流的工具函数，可以处理一些复杂的场景：

```javascript
function throttle(func, delay, options = {}) {
  let lastTime = 0;
  let timeoutId;
  let lastArgs;
  let lastContext;
  let result;
  
  function clear() {
    clearTimeout(timeoutId);
    timeoutId = null;
    lastTime = 0;
    lastArgs = null;
    lastContext = null;
  }
  
  function later() {
    const now = Date.now();
    const elapsed = now - lastTime;
    if (elapsed < delay && elapsed >= 0) {
      timeoutId = setTimeout(later, delay - elapsed);
    } else {
      clear();
      result = func.apply(lastContext, lastArgs);
      if (!timeoutId) {
        lastContext = null;
        lastArgs = null;
      }
    }
  }
  
  return function() {
    const now = Date.now();
    const isImmediate = options.immediate && lastTime === 0;
    lastArgs = arguments;
    lastContext = this;
    
    if (isImmediate) {
      result = func.apply(lastContext, lastArgs);
      lastTime = now;
    } else {
      if (!timeoutId) {
        timeoutId = setTimeout(later, delay);
        lastTime = now;
      }
    }
    
    return result;
  };
}
```

这个函数接受三个参数：`func`是要执行的函数，`delay`是节流的时间间隔，单位为毫秒，`options`是一个可选的配置对象，可以包含一个布尔值属性`immediate`，表示是否立即执行`func`函数。

当调用节流函数返回的新函数时，它会使用`setTimeout()`函数来延迟执行`func`函数。如果在延迟时间内多次调用新函数，则会忽略这些调用，直到延迟时间结束后才会执行一次`func`函数。如果配置对象中的`immediate`属性为`true`，则会在第一次调用新函数时立即执行`func`函数，并在延迟时间内忽略后续的调用。

该函数还提供了一些额外的功能：

- 在延迟时间内多次调用新函数时，只会保留最后一次调用的参数和上下文，并在延迟时间结束后使用这些参数和上下文执行一次`func`函数。
- 如果在延迟时间内调用新函数时立即清除了定时器，则会重置计时器，并在下一次调用新函数时重新开始计时。
- 如果在延迟时间内调用新函数时立即清除了定时器，并且在延迟时间结束前没有再次调用新函数，则会清除保存的参数和上下文。

这些功能可以处理一些复杂的场景，例如处理异步操作或者需要传递参数的情况。在实际应用中，应该根据具体场景选择更加适合的节流方案。

### TS实现

以下是一个用TypeScript实现的节流的工具函数，可以处理一些复杂的场景：

```typescript
interface ThrottleOptions {
  immediate?: boolean;
}

function throttle<T extends (...args: any[]) => void>(func: T, delay: number, options: ThrottleOptions = {}): (...args: Parameters<T>) => void {
  let lastTime = 0;
  let timeoutId: ReturnType<typeof setTimeout>;
  let lastArgs: Parameters<T> | null = null;
  let lastContext: unknown | null = null;
  let result: ReturnType<T> | undefined;
  
  function clear() {
    clearTimeout(timeoutId);
    timeoutId = null as any;
    lastTime = 0;
    lastArgs = null;
    lastContext = null;
  }
  
  function later() {
    const now = Date.now();
    const elapsed = now - lastTime;
    if (elapsed < delay && elapsed >= 0) {
      timeoutId = setTimeout(later, delay - elapsed);
    } else {
      clear();
      result = func.apply(lastContext, lastArgs!);
      if (!timeoutId) {
        lastContext = null;
        lastArgs = null;
      }
    }
  }
  
  return function(this: unknown, ...args: Parameters<T>): void {
    const now = Date.now();
    const isImmediate = options.immediate && lastTime === 0;
    lastArgs = args;
    lastContext = this;
    
    if (isImmediate) {
      result = func.apply(lastContext, lastArgs);
      lastTime = now;
    } else {
      if (!timeoutId) {
        timeoutId = setTimeout(later, delay);
        lastTime = now;
      }
    }
    
    return result as any;
  };
}
```

这个函数与上面的JavaScript版本的函数基本相同，只是在参数和返回值声明时添加了类型注解。参数`func`被注解为一个泛型函数类型，其参数类型和返回值类型与原函数一致。参数`delay`被注解为一个数字类型，`options`被注解为一个可选的配置对象类型，包含一个布尔值属性`immediate`，表示是否立即执行`func`函数。



## 指定范围随机数

### JS实现

以下是一个用JS编写的指定范围随机数的工具函数：

```javascript
function randomInRange(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
```

这个函数接受两个参数：`min`和`max`，表示要生成的随机数的范围。函数使用`Math.random()`函数生成一个0到1之间的随机数，然后将其乘以`(max - min + 1)`，再加上`min`，得到一个在`[min, max]`范围内的随机数。最后使用`Math.floor()`函数将其向下取整，以保证返回值是一个整数。

这个函数可以用于生成指定范围内的随机整数，例如：

```javascript
const randomNum = randomInRange(1, 10);
console.log(randomNum); // 可能输出1到10之间的任意整数
```

### TS实现

以下是一个用TypeScript实现的指定范围随机数的工具函数：

```typescript
function randomInRange(min: number, max: number): number {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

/**
 * 生成指定范围内的随机整数
 * @param min 随机数范围的最小值
 * @param max 随机数范围的最大值
 * @returns 指定范围内的随机整数
 */
function randomInRange(min: number, max: number): number {
  // 生成一个0到1之间的随机数，并将其乘以(max - min + 1)，得到一个在[min, max]范围内的随机数
  const randomNum = Math.random() * (max - min + 1);
  // 将随机数向下取整，以保证返回值是一个整数
  const floorNum = Math.floor(randomNum);
  // 将随机数加上min，得到在[min, max]范围内的随机整数
  const result = floorNum + min;
  // 返回结果
  return result;
}

```

这个函数与上面的JavaScript版本的函数基本相同，只是在参数和返回值声明时添加了类型注解。参数`min`和`max`被注解为数字类型，返回值被注解为数字类型。



