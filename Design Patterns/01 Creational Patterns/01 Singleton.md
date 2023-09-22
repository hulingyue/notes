# 单例模式

## 饿汉模式
``` cpp
class Singleton {
public:
    static Singleton* get_instance() {
        return Singleton::instance;
    }
private:
    Singleton() {};

private:
    static Singleton* instance;
};


Singleton* Singleton::instance = new Singleton();
```

## 懒汉模式
1. 静态函数的静态局部变量
    > C++11之后，静态函数的静态局部变量初始化具有线程安全性。
    ``` cpp
    class Singleton {
    public:
        static Singleton* get_instance() {
            static Singleton obj;
            return &obj;
        }

    private:
        Singleton() {}
    };
    ```
2. 互斥锁 + 双重检查
   ``` cpp
    class Singleton {
    public:
        static Singleton* get_instance() {
            if (Singleton::instance == nullptr) {
                Singleton::mtx.lock();
                if (Singleton::instance == nullptr) {
                    Singleton::instance = new Singleton();
                }
                Singleton::mtx.unlock();
            }
            return Singleton::instance;
        }

    private:
        Singleton() {}

    private:
        static Singleton* instance;
        static std::mutex mtx;
    };

    Singleton* Singleton::instance = nullptr;
    std::mutex Singleton::mtx;
   ```