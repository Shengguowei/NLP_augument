~~ 1 .盛国威  ~~

1. 输出需要的数据结构。

2. 发现明明设定了自己上传，还是要手工操作

3. 发现有的时候为什么print可以而print_function不可以，是因为代码是2.7的，而3才能用print(),如果可以
是因为加了__future_print_

4. 现在重写输出文件

5. 自然语言处理中，为什么百度翻译可以提升效果？
   1. 是扩展数据集。
   2. 是增强百度翻译迁移学习。
   3. 百度翻译是在干什么?他的翻译是有准确率的差异的。有85%的差异。
   4.


# 测试：

    使用新代码后，在原始数据上结果为：
    main_accuracy :0.979228
    valid_accuracy:0.888

    使用原版代码，在新数据集上结果为
    main_accuracy:  0.979228
    valid_accuracy: 0.888

    如果一致，证明，对代码的修改没有错误。

     使用translate+KG发生的现象:
     main_accuracy:
     0.99578
     valid_accuracy:
     0.796

# 19年5月10日：
    1. 验证_验证集的结果是否正确？
       原始代码+raw_content：     结果：main_accuray 0.979228  validation_accuray 0.888
       新版代码结果+raw_content：  结果：main_accuray 0.979228  validation_accuray 0.888
       结果相同，但两次训练的结果完全相同，这是在哪里有问题吧?

    2. translate之后的结果是？
       main_accuray 0.949816    validation_accuray 0.844

    3. kg之后的结果是什么？
       main_accuray 0.993164    validation_accuray 0.856

    4. translate + kg的结果是什么？
       main_accuray    validation_accuray
       0.99578                  0.796








    为什么会导致这样的结果？哪些被分类错了？哪些被分类对了？
    1.解决问题1，在这个数据集中，validation是怎么计算的，用测试集吗？
        validation证明是测试集的结果。（代码，及测试集数量佐证）
        当是validation是true的时候，有训练集的结果。

    2.解决问题2，输出分类结果。
      在输出了分类结果后，我们发现，输出的准确率是0.752，虽然与0.796不同，但仍然在一个数量级上（有必要调查一下，为什么评估的值不同。）
      输出的方法是直接用分类器的predict的结果进行的分类。

    3.解决问题3，为什么会有分类问题？
        猜测1：破坏数据分布。
        猜测2：增加新的词。
        猜测3：添加噪音。

    4.解决问题4：
        分类出现问题的句子有哪些特征？
        输入到模型中又能成什么样子？

    5.对错误的句子怎么分析？
        是什么导致的这些错误？
        整个过程是如何决定的？决定的过程中哪里出了问题？哪个神经元它不能用了？错误句子中的词出现了偏差？
        翻译的中间件有问题？

    6.什么样的句子出问题的多？在输入端口怎么出的问题？

    7.理论上加了KG以后，实体的数量会变多，但在这里，却依旧有大量的词不认识，如何有效的加词。

    8.何不KG后，再加translate
      假设KG能补上KG的句子

    9.或者是很漂亮的模型，或者是很好的实验效果。









    2. 方法_

    3. 无情感词的一些处理方法是怎么做的？


    # 今天蛮开心的。
    # 当陆梓瀚说到平衡样本集的时候，我没有get到他准确的意思，却施加以反对的意见，这不对。
    # 但做的好的一点是，我后来仔细思索了他的想法。
    # 不要犹豫，不要拖延。

    1.我现在对数据做一下平衡数据集。
    2.将PPT彻底做出来。


    # 5月22日
       我发现写的平衡数据集的代码有问题，前面的实验全部需要重做
       问题在：我平衡数据集的逻辑出现问题。
       已经完成修改。
       前面的实验可能都要重跑。

       在当前实验中，
       "TREC_train_kg_balance_result.txt"
       是实验结果。

       牢记一点是，新生成的数据集，并没有增加原始数据集。


       # 在平衡了数据集之后
       # 我们发现效果反而变差了

       #
       main_accuray    validation_accuray
        0.980839            0.808
       没有加入原始数据集。
       故导致变差

       #
       main_accuray    validation_accuray
        0.980839            0.808


        # 在第33论就停止，不知道是不是。


        # 平衡了误差，并且加上了原始的数据集，发现
       main_accuray    validation_accuray
        0.986385            0.876

        # 这是没有调参的结果。
          但如果想要论证有效性，一般是不调参的。
          见论文。

        # 1.珍惜百度翻译宝贵机会，再跑一个数据集
          2.分析过去跑的实验姿势
          3.百度一下数据集
          4.现在开始整理，现在开始
          5.模型输出图像


    // 下载的原始文件存储的位置
    '/home/guowei/.chainer/dataset/_dl_cache'
    'e5eb72af713d09fd07dc67d56b41d4a1'

    完成数据集，发现抽样比例不对。
    因此进行数据平衡，代码保存在数据平衡文件夹下

    在优化数据平衡函数后，对实验的再次运行。


name |age | time
---- |--- |-----
  a | b   |c





