# 匹配性问题

1. 如果两个对象相等，那他们的hashcode一定相同。这里的相等指的是 ==
2. 如果两个对象的hashcode相等，他俩不一定==。这时候要去判断equals方法
    
    这也是Map的判断规则，hashcode相等 && equals为true。hashcode用来确定Map里的桶，equals用来确定桶里面的线性查找。
3. 所以equals方法要重写不同对象各属性的相等，hashcode方法要重写相同属性的hash值，一定要用对象的属性去获取hashcode，而不是这个对象本身。