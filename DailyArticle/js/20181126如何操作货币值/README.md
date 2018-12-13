# 概述(介绍dinero库)

1. https://frontstuff.io/how-to-handle-monetary-values-in-javascript
2. 2018.4.13
3. 每天都在使用货币，但没有操作货币值的公认编程方式
4. 货币值经常使用，但没有一个像date或time等的object表示

## 读后总结

1. 介绍dinero这个库
2. 利用小数转整数可以处理精度问题

## 用number数值表示货币的缺陷

1. 如10，没有10‘钱’这样的东西，它是10美元或人民币，想用不同货币需要先进行换算

2. 运算会出现问题，货币有小数，但js的小数运算会出现问题（0.1+0.2 = 0.30000000000000004 ），解决方式

   - 将float以strings处理，如Decimal.js
   - 将小数*100变为整数再除以100，但这样需要额外计算

3. 比如，999块钱打5折，499.995,需要四舍五入到500，普通的运算无法实现

## dinero.js

1. https://github.com/sarahdayan/dinero.js

2. 2k stars 

3. 全局设置，如Dinero.globalLocale = 'de-DE'，可以将所有使用到的值都设置为美元

4. 不可变数据与链式操作，不可变数据：如下调用priceWithTax，price值并不会改变

   ```javascript
    const vm = new Vue({
      data: {
        price: Dinero({ amount: 500 })
      },
      computed: {
        priceWithTax() {
          return this.price.add(this.price.percentage(10))
        }
      }
    })
   ```
