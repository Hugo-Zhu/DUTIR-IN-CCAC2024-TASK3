# DUTIR-IN-CCAC2024-TASK3
# 《基于用户画像的中文情绪分类》评测报告
## 任务描述
 给定一个用户画像（包括用户所在的地区、性别、关注人列表、发表的历史文本等）以及一个用户文本，参赛模型需判断用户文本所表达的情绪，输出的情绪是下面五种情绪之一：喜、哀、惊、恐、怒。
### 数据样例：

##### 输入：
**用户画像**
    - 地区：上海
    - 性别：女
    - 关注的人列表：...
    - 用户发表的历史文本列表：...
**推文**
    - 刚刚买的新裙子，真的超级好看，我简直爱死了！
##### 输出：
喜

评价指标： Macro-F1 score

$F1_{macro} = \frac{1}{N} \sum_{i=1}^{N} F1_i$

其中，$N$是类别数量，$F1_i$是第i类的F1分数

## 任务定义:
输入:
1. 待预测文本$x$
2. 用户数据$u$
    - 用户ID $u_{id}$
    - 用户信息 $u_{info}$：位置，性别
    - 用户历史推文 $u_{his} = \{ p_1, p_2, ... p_N \}$
    - 用户昵称 $u_{name}$
    - 用户社交网络：关注类标，被关注列表...

输出:
    用户对于文本 $x$ 的情感 $y = f(x, u)$
## baselines
### 1.基于bert-base-chinese预训练模型进行微调
参考https://github.com/shuxinyin/Chinese-Text-Classification/tree/master/bert_classification
```
baseline/bert-base-chinese/raw data/100 epoch/lr 0.005
loss: 0.7072446474432945
              precision    recall  f1-score   support

           喜     0.8195    0.8926    0.8545       773
           哀     0.7444    0.8200    0.7804       650
           惊     0.6500    0.2989    0.4094        87
           恐     1.0000    0.0000    0.0000        42
           怒     0.6857    0.4768    0.5625       151

    accuracy                         0.7757      1703
   macro avg     0.7799    0.4977    0.5214      1703
weighted avg     0.7748    0.7757    0.7565      1703
```
### 2.使用zero-shot对qwen7b模型直接进行问答
```
llm zero-shot/qwen1.5-7b/5 epoch
              precision    recall  f1-score   support

           喜     0.6372    0.7215    0.6768       650
           哀     0.8048    0.6934    0.7450       773
           惊     0.5370    0.9139    0.6765       151
           恐     0.4000    0.3333    0.3636        42
           怒     0.7778    0.0805    0.1458        87

    accuracy                         0.6835      1703
   macro avg     0.6314    0.5485    0.5215      1703
weighted avg     0.7057    0.6835    0.6728      1703
```
