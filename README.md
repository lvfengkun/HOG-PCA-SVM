# HOG-PCA-SVM
HOG+SVM+PCA的训练及测试代码，使用的是sklearn框架，人脸数据集为lfw_funneled，最后效果：PCA+SVM:85，HOG+SVM:94,SVM+PCA+HOG:92

各部分输出：
（1）PCA+SVM
Total dataset size:
n_samples: 1288
n_features: 1850
n_classes: 7
Extracting the top 100 eigenfaces from 966 faces
done in 0.435s
Projecting the input data on the eigenfaces orthonormal basis
(966, 100)
(322, 100)
done in 0.018s
Fitting the classifier to the training set
done in 23.820s
Best estimator found by grid search:
SVC(C=1000.0, class_weight='balanced', gamma=0.005)
5
Predicting people's names on the test set
done in 0.039s
[3]
3
                   precision    recall  f1-score   support
     Ariel Sharon       0.67      0.77      0.71        13
     Colin Powell       0.83      0.90      0.86        60
  Donald Rumsfeld       0.85      0.63      0.72        27
    George W Bush       0.89      0.97      0.93       146
Gerhard Schroeder       0.90      0.76      0.83        25
      Hugo Chavez       0.90      0.60      0.72        15
       Tony Blair       0.87      0.75      0.81        36
         accuracy                           0.86       322
        macro avg       0.84      0.77      0.80       322
     weighted avg       0.86      0.86      0.86       322
[[ 10   0   1   2   0   0   0]
 [  1  54   0   4   0   1   0]
 [  3   2  17   5   0   0   0]
 [  0   4   0 142   0   0   0]
 [  0   1   1   1  19   0   3]
 [  0   3   0   1   1   9   1]
 [  1   1   1   5   1   0  27]]

可以看到，训练模型的时间为23.820s，训练结果为平均精度达到了0.86，混淆矩阵显示1号（样本13人）检测到14人，其中正确的人数为10人，另有1人为2号，3人为3号，正确的1号样本有1人被检测成了3号，2人被检测成了4号。
（2）HOG+SVM
train
done in 1739.726s
Best estimator found by grid search:
SVC(C=1000.0, cache_size=200, class_weight='balanced', coef0=0.0,
  decision_function_shape='ovr', degree=3, gamma=0.0001, kernel='rbf',
  max_iter=-1, probability=False, random_state=None, shrinking=True,
  tol=0.001, verbose=False)
   		 precision    recall  f1-score   support

     Ariel Sharon       1.00      0.85      0.92        13
     Colin Powell       0.94      1.00      0.97        60
  Donald Rumsfeld       0.92      0.81      0.86        27
    George W Bush       0.94      0.99      0.96       146
Gerhard Schroeder       0.92      0.96      0.94        25
      Hugo Chavez       1.00      0.67      0.80        15
       Tony Blair       0.94      0.83      0.88        36

      avg / total       0.94      0.94      0.94       322

[[ 11   0   1   1   0   0   0]
 [  0  60   0   0   0   0   0]
 [  0   1  22   2   1   0   1]
 [  0   0   1 145   0   0   0]
 [  0   0   0   1  24   0   0]
 [  0   1   0   3   0  10   1]
 [  0   2   0   3   1   0  30]]

可以看到，训练模型的时间为1739.726s（大概半个小时），平均准确度达到0.94。从混淆矩阵中可以看到1号与6号出现了明显的过拟合现象。
（3）HOG+PCA+SVM
train
done in 17.062s
Best estimator found by grid search:
SVC(C=1000.0, cache_size=200, class_weight='balanced', coef0=0.0,
  decision_function_shape='ovr', degree=3, gamma=0.005, kernel='rbf',
  max_iter=-1, probability=False, random_state=None, shrinking=True,
  tol=0.001, verbose=False)

                   precision    recall  f1-score   support

     Ariel Sharon       1.00      0.85      0.92        13
     Colin Powell       0.90      1.00      0.94        60
  Donald Rumsfeld       0.79      0.81      0.80        27
    George W Bush       0.93      0.97      0.95       146
Gerhard Schroeder       0.96      0.88      0.92        25
      Hugo Chavez       0.91      0.67      0.77        15
       Tony Blair       0.97      0.81      0.88        36

      avg / total       0.92      0.92      0.91       322

[[ 11   0   1   1   0   0   0]
 [  0  60   0   0   0   0   0]
 [  0   1  22   2   1   0   1]
 [  0   0   5 141   0   0   0]
 [  0   1   0   1  22   1   0]
 [  0   1   0   4   0  10   0]
 [  0   4   0   3   0   0  29]]

可以看到模型的训练时间为17.062s，远小于HOG+SVM的训练速度，从精度方面，平均精度为0.92，从混淆矩阵中可以看到，1号与6号的过拟合现象已经明显减弱。
