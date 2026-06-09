先从文件夹介绍起：

_config.yml 和 LICENSE 文件夹可以直接忽略.



requirements.txt 文件介绍程序所用的库的版本

torch == 0.4.1
torchvision == 0.2.1
如果连这两个库都不认识的请移步官网看详解：

torch - PyTorch 1.8.0 documentation

torchvision - Torchvision master documentation



README.md 文件记录了github代码贡献者对整个工程的详解。（文档作用）



data 文件夹用来存放相应的数据，可以发现一开始里面是 mnist 和 cifar 的空文件夹，在待会儿代码讲解过程中会提到怎么加载数据。

因为是个从零开始系列，所以这里用的都是最简单的 MNIST 和 CIFAR-10 数据集，如果对这两个数据集不了解，可以自行检索查看具体数据格式和内容。



save 文件夹用来存放最后生成的一系列结果，比方说自己定义的 loss 和 accuracy 随通信次数的可视化显示。



models 里面有Fed.py 用来将模型平均实现 FedAvg、Net.py 定义不同的神经网络类型如 MLP、CNN等、test.py 将最后得到的模型效果拿来测试、update.py 用来定义本地更新的内容.



utils 里面的options.py用来存放程序的一些超参数的值，方便在程序运行过程中直接调节(不理解的可以在后面看解释)、sampling.py用来对Non-IID的数据分布进行采样的模拟(不懂的可以先放着，后面会解释)。



main_nn.py 和 main_fed.py 就是最后用来跑的那个程序，其他部分都是拼图玩具，把这些代码实现的部分功能拼接在一起构成了整个实验流程。

