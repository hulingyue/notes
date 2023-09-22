# 工厂方法模式 & 抽象工厂方法
> 两者区别不大，一定要区别两者差异显得过于教条，实用为主，合并记录
``` cpp
#include <iostream>


class AbstractProduct {
public:
    virtual std::string name() = 0;
};

class ProductA : public AbstractProduct {
public:
    std::string name() {
        return "ProductA";
    }
};

class ProductB : public AbstractProduct {
public:
    std::string name() {
        return "ProductB";
    }
};

class AbstractFactory {
public:
    virtual AbstractProduct* product() = 0;
};

class FactoryA : public AbstractFactory {
public:
    AbstractProduct* product() {
        return new ProductA;
    }
};


class FactoryB : public AbstractFactory {
public:
    AbstractProduct* product() {
        return new ProductB;
    }
};

int main() {

    AbstractFactory* factoryA = new FactoryA;
    std::cout << factoryA->product()->name() << std::endl;

    AbstractFactory* factoryB = new FactoryB;
    std::cout << factoryB->product()->name() << std::endl;
    return 0;
}

/******************/
/** 输出结果：    **
 ** ProductA     **
 ** ProductB     **/
/******************/
```
