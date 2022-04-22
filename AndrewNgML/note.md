# Machine Learning

## Supervised Learning

regression problem: continuous data

classification problem: discrete data

## Unsupervised Learning

just give the data, no more.

Cocktail party problem algorithm

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211017172628252.png" alt="image-20211017172628252" style="zoom:67%;" />

(奇异值分解)

## Linear regression with one variable

### cost function

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211018095047352.png" alt="image-20211018095047352" style="zoom:67%;" />

### Gradient descent

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211019000445547.png" alt="image-20211019000445547" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211018235824996.png" alt="image-20211018235824996" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211019003906910.png" alt="image-20211019003906910" style="zoom:67%;" />

"Batch" Gradient Decent

"Batch": Each step of gradient descent uses all the training example

## Linear regression with multiple variables

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211019170543787.png" alt="image-20211019170543787" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211019171019755.png" alt="image-20211019171019755" style="zoom:67%;" />

### Mean normalization

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211019184013906.png" alt="image-20211019184013906" style="zoom:67%;" />

## Learning rate

### correct

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211020001020177.png" alt="image-20211020001020177" style="zoom:67%;" />

### incorrect

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211020001054689.png" alt="image-20211020001054689" style="zoom:67%;" />

### Summary

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211020001213596.png" alt="image-20211020001213596" style="zoom:67%;" />

## Normal equation

Method to solve for  $\theta$ analytically

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211020005314572.png" alt="image-20211020005314572" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211020010145741.png" alt="image-20211020010145741" style="zoom:67%;" />

**no need to do feature scaling**

## Gradient Descent vs Normal Equation

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211020011220027.png" alt="image-20211020011220027" style="zoom:67%;" />

## Non-invertible

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211020124147871.png" alt="image-20211020124147871" style="zoom:67%;" />

## Logistic Regression

### Hypothesis Representation

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023005007316.png" alt="image-20211023005007316" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023005054293.png" alt="image-20211023005054293" style="zoom:67%;" />

### Decision boundary

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023010552209.png" alt="image-20211023010552209" style="zoom:67%;" />

### Cost function

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023112558770.png" alt="image-20211023112558770" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023112725427.png" alt="image-20211023112725427" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023112836440.png" alt="image-20211023112836440" style="zoom:67%;" />

### 	Simplified cost function

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023115428347.png" alt="image-20211023115428347" style="zoom:67%;" />

### Gradient descent

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023115555531.png" alt="image-20211023115555531" style="zoom:67%;" />

### Advanced optimization

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023145228396.png" alt="image-20211023145228396" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023145342174.png" alt="image-20211023145342174" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023145415795.png" alt="image-20211023145415795" style="zoom:67%;" />

### Multi-class classification: One-vs-all

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023150442892.png" alt="image-20211023150442892" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211023150507839.png" alt="image-20211023150507839" style="zoom:67%;" />

## Regularization

### The problem of overfitting

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025012436700.png" alt="image-20211025012436700" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025012502310.png" alt="image-20211025012502310" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025012534080.png" alt="image-20211025012534080" style="zoom:67%;" />

### Cost function

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025014036511.png" alt="image-20211025014036511" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025014119409.png" alt="image-20211025014119409" style="zoom:67%;" />

### Regularized linear regression

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025110223492.png" alt="image-20211025110223492" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025110339838.png" alt="image-20211025110339838" style="zoom:67%;" />

### Regularized logistic regression

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025111909042.png" alt="image-20211025111909042" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025111940695.png" alt="image-20211025111940695" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211025112208890.png" alt="image-20211025112208890" style="zoom:67%;" />

## Neural Networks

### Model representation

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211026163612279.png" alt="image-20211026163612279" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211026163644823.png" alt="image-20211026163644823" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211026163739103.png" alt="image-20211026163739103" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027093843005.png" alt="image-20211027093843005" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027094029967.png" alt="image-20211027094029967" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027094216086.png" alt="image-20211027094216086" style="zoom:67%;" />

### Examples and intuitions

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027101614371.png" alt="image-20211027101614371" style="zoom:67%;" />

### Multi-class classification

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027102354470.png" alt="image-20211027102354470" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027102416164.png" alt="image-20211027102416164" style="zoom:67%;" />

### Cost function

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027105103105.png" alt="image-20211027105103105" style="zoom:67%;" />

### Backpropagation algorithm

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027151430926.png" alt="image-20211027151430926" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027151741977.png" alt="image-20211027151741977" style="zoom:67%;" />

### Backpropagation intuition

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027154815024.png" alt="image-20211027154815024" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027155151270.png" alt="image-20211027155151270" style="zoom:67%;" />

### Unrolling parameters

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027164349705.png" alt="image-20211027164349705" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027164418254.png" alt="image-20211027164418254" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027164454184.png" alt="image-20211027164454184" style="zoom:67%;" />

### Gradient checking

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027170558890.png" alt="image-20211027170558890" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027170630492.png" alt="image-20211027170630492" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027170736450.png" alt="image-20211027170736450" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211027170800159.png" alt="image-20211027170800159" style="zoom:67%;" />

### Random initialization

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211028003457676.png" alt="image-20211028003457676" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211028003941710.png" alt="image-20211028003941710" style="zoom:67%;" />

### Putting it together

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211028020603807.png" alt="image-20211028020603807" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211028020830137.png" alt="image-20211028020830137" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211028020917706.png" alt="image-20211028020917706" style="zoom:67%;" />



## Advice for applying machine learning

### Deciding what to try next

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103121105750.png" alt="image-20211103121105750" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103121209460.png" alt="image-20211103121209460" style="zoom:67%;" />

### Evaluating a hypothesis

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103122516683.png" alt="image-20211103122516683" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103122543960.png" alt="image-20211103122543960" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103122725365.png" alt="image-20211103122725365" style="zoom:67%;" />

### Model selection and training/validation/test sets

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103130221710.png" alt="image-20211103130221710" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103130341138.png" alt="image-20211103130341138" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103130510335.png" alt="image-20211103130510335" style="zoom:67%;" />

### Diagnosing bias vs. variance

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103132056309.png" alt="image-20211103132056309" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103132213355.png" alt="image-20211103132213355" style="zoom:67%;" />

### Regularization and bias/variance

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103135233132.png" alt="image-20211103135233132" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103135315501.png" alt="image-20211103135315501" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103135457325.png" alt="image-20211103135457325" style="zoom:67%;" />

### Learning curves

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103143648567.png" alt="image-20211103143648567" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103143725551.png" alt="image-20211103143725551" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103143811004.png" alt="image-20211103143811004" style="zoom:67%;" />

### Deciding what to try next(revisited)

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103145333844.png" alt="image-20211103145333844" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103145432106.png" alt="image-20211103145432106" style="zoom:67%;" />

## Machine learning system design

### Error analysis

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103234849732.png" alt="image-20211103234849732" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103234927199.png" alt="image-20211103234927199" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211103235028681.png" alt="image-20211103235028681" style="zoom:67%;" />

### Error metrics for skewed classes

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211104002007911.png" alt="image-20211104002007911" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211104002224836.png" alt="image-20211104002224836" style="zoom:67%;" />

### Trading off precision and recall

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211104005732010.png" alt="image-20211104005732010" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211104005815269.png" alt="image-20211104005815269" style="zoom:67%;" />

### Data for machine learning

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211104173123286.png" alt="image-20211104173123286" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211104173207819.png" alt="image-20211104173207819" style="zoom:67%;" />

## Support Vector Machines

### Optimization objective

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211108155452964.png" alt="image-20211108155452964" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211108155551469.png" alt="image-20211108155551469" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211108155803363.png" alt="image-20211108155803363" style="zoom:67%;" />

### Large Margin Intuition

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211108174608326.png" alt="image-20211108174608326" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109075121790.png" alt="image-20211109075121790" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211108174730488.png" alt="image-20211108174730488" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211108174830833.png" alt="image-20211108174830833" style="zoom:67%;" />

### The mathematics behind large margin classification

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109013157129.png" alt="image-20211109013157129" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109013325503.png" alt="image-20211109013325503" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109013751025.png" alt="image-20211109013751025" style="zoom:67%;" />

### Kernels

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109020752481.png" alt="image-20211109020752481" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109020840057.png" alt="image-20211109020840057" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109020926952.png" alt="image-20211109020926952" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109021052770.png" alt="image-20211109021052770" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109021424270.png" alt="image-20211109021424270" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109081702796.png" alt="image-20211109081702796" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109081752847.png" alt="image-20211109081752847" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109081848062.png" alt="image-20211109081848062" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109081915169.png" alt="image-20211109081915169" style="zoom:67%;" />

### Using an SVM

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109135409008.png" alt="image-20211109135409008" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109135616653.png" alt="image-20211109135616653" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109140126862.png" alt="image-20211109140126862" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109140317833.png" alt="image-20211109140317833" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211109140436902.png" alt="image-20211109140436902" style="zoom:67%;" />

## Clustering

### Unsupervised learning introduction

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112081804874.png" alt="image-20211112081804874" style="zoom:67%;" />

###  K-means algorithm

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112112612968.png" alt="image-20211112112612968" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112112803731.png" alt="image-20211112112803731" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112112953527.png" alt="image-20211112112953527" style="zoom:67%;" />

### Optimization objective

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112115007325.png" alt="image-20211112115007325" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112115044844.png" alt="image-20211112115044844" style="zoom:67%;" />

### Random initialization

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112124051716.png" alt="image-20211112124051716" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112124119552.png" alt="image-20211112124119552" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112124242764.png" alt="image-20211112124242764" style="zoom:67%;" />

### Choosing the number of clusters

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112132720038.png" alt="image-20211112132720038" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112132758146.png" alt="image-20211112132758146" style="zoom:67%;" />

## Dimensionality Reduction

### Motivation 1: Data Compression

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112175333758.png" alt="image-20211112175333758" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112175420941.png" alt="image-20211112175420941" style="zoom:67%;" />

### Motivation 2: Data Visualization

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112192034787.png" alt="image-20211112192034787" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112192057322.png" alt="image-20211112192057322" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112192140828.png" alt="image-20211112192140828" style="zoom:67%;" />

### Principal Component Analysis problem formulation

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112205410988.png" alt="image-20211112205410988" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112205511114.png" alt="image-20211112205511114" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211112205552522.png" alt="image-20211112205552522" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113164538017.png" alt="image-20211113164538017" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113164639274.png" alt="image-20211113164639274" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113164717565.png" alt="image-20211113164717565" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113164913781.png" alt="image-20211113164913781" style="zoom:67%;" />

### Choosing the number of principal components

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113170915650.png" alt="image-20211113170915650" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113170957368.png" alt="image-20211113170957368" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113171056072.png" alt="image-20211113171056072" style="zoom:67%;" />

### Reconstruction from compressed representation

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113171949102.png" alt="image-20211113171949102" style="zoom:67%;" />

### Advice for applying PCA

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113174215666.png" alt="image-20211113174215666" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113174243101.png" alt="image-20211113174243101" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113174312899.png" alt="image-20211113174312899" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211113174356198.png" alt="image-20211113174356198" style="zoom:67%;" />

## Anomaly detection

### Problem motivation

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211115134146855.png" alt="image-20211115134146855" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211115134233413.png" alt="image-20211115134233413" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211115134335805.png" alt="image-20211115134335805" style="zoom:67%;" />

### Gaussian distribution

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211115140029411.png" alt="image-20211115140029411" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211115140054380.png" alt="image-20211115140054380" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211115140238943.png" alt="image-20211115140238943" style="zoom:67%;" />

### Algorithm

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116022638728.png" alt="image-20211116022638728" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116022833385.png" alt="image-20211116022833385" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116022947737.png" alt="image-20211116022947737" style="zoom:67%;" />

### Developing and evaluating an anomaly detection system

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116105619126.png" alt="image-20211116105619126" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116105706002.png" alt="image-20211116105706002" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116111042793.png" alt="image-20211116111042793" style="zoom:67%;" />

### Anomaly  detection vs. supervised learning

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116114549056.png" alt="image-20211116114549056" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116114632525.png" alt="image-20211116114632525" style="zoom:67%;" />

### Choosing what features to use

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116131008852.png" alt="image-20211116131008852" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116131117264.png" alt="image-20211116131117264" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116131143298.png" alt="image-20211116131143298" style="zoom:67%;" />

### Multivariate Gaussian distribution

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116134246414.png" alt="image-20211116134246414" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116134315961.png" alt="image-20211116134315961" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116134355564.png" alt="image-20211116134355564" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116134422275.png" alt="image-20211116134422275" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116134446938.png" alt="image-20211116134446938" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116134513205.png" alt="image-20211116134513205" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116134548166.png" alt="image-20211116134548166" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116134616627.png" alt="image-20211116134616627" style="zoom:67%;" />

### Anomaly detection using the multivariate Gaussian distribution

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116143329827.png" alt="image-20211116143329827" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116143432504.png" alt="image-20211116143432504" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116143646392.png" alt="image-20211116143646392" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211116144522813.png" alt="image-20211116144522813" style="zoom:67%;" />

## Recommender Systems

### Problem formulation

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081118183.png" alt="image-20211118081118183" style="zoom:67%;" />

### Content-based recommendations

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081237960.png" alt="image-20211118081237960" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081314061.png" alt="image-20211118081314061" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081359693.png" alt="image-20211118081359693" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081430434.png" alt="image-20211118081430434" style="zoom:67%;" />

### Collaborative filtering

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081537387.png" alt="image-20211118081537387" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081608538.png" alt="image-20211118081608538" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081642704.png" alt="image-20211118081642704" style="zoom:67%;" />

### Collaborative filtering algorithm

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081806795.png" alt="image-20211118081806795" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081844679.png" alt="image-20211118081844679" style="zoom:67%;" />

### Vectorization: Low rank matrix factorization

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118081945359.png" alt="image-20211118081945359" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118082017534.png" alt="image-20211118082017534" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118082043414.png" alt="image-20211118082043414" style="zoom:67%;" />

### Implementational detail: Mean normalization

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118082227239.png" alt="image-20211118082227239" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211118082259754.png" alt="image-20211118082259754" style="zoom:67%;" />

## Large scale machine learning

### Learning with large datasets

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211120192645116.png" alt="image-20211120192645116" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211120192743149.png" alt="image-20211120192743149" style="zoom:67%;" />

### Stochastic gradient descent

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211120195146691.png" alt="image-20211120195146691" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211120195240487.png" alt="image-20211120195240487" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211120195333941.png" alt="image-20211120195333941" style="zoom:67%;" />

### Mini-batch gradient descent

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121102456468.png" alt="image-20211121102456468" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121102537055.png" alt="image-20211121102537055" style="zoom:67%;" />

### Stochastic gradient descent convergence

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121105949407.png" alt="image-20211121105949407" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121110046031.png" alt="image-20211121110046031" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121110212561.png" alt="image-20211121110212561" style="zoom:67%;" />

### Online learning

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121112333012.png" alt="image-20211121112333012" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121112621010.png" alt="image-20211121112621010" style="zoom:67%;" />

### Map-reduce and data parallelism

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121115538762.png" alt="image-20211121115538762" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121115602815.png" alt="image-20211121115602815" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121115712979.png" alt="image-20211121115712979" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121115829602.png" alt="image-20211121115829602" style="zoom:67%;" />

## Application example: Photo OCR

### Problem description and pipeline

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121224115903.png" alt="image-20211121224115903" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121224219866.png" alt="image-20211121224219866" style="zoom:67%;" />

### Sliding windows

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121231212303.png" alt="image-20211121231212303" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121231257396.png" alt="image-20211121231257396" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121231320913.png" alt="image-20211121231320913" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121231442940.png" alt="image-20211121231442940" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121231530375.png" alt="image-20211121231530375" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121231622983.png" alt="image-20211121231622983" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211121231737268.png" alt="image-20211121231737268" style="zoom:67%;" />

### Getting lots of data: Artificial data synthesis

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122013448456.png" alt="image-20211122013448456" style="zoom:67%;" />



<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122013513088.png" alt="image-20211122013513088" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122013539131.png" alt="image-20211122013539131" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122013611355.png" alt="image-20211122013611355" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122013642622.png" alt="image-20211122013642622" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122013937421.png" alt="image-20211122013937421" style="zoom:67%;" />

### Ceiling analysis: What part of the pipeline to work on next

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122015916983.png" alt="image-20211122015916983" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122015955061.png" alt="image-20211122015955061" style="zoom:67%;" />

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122020035241.png" alt="image-20211122020035241" style="zoom:67%;" />

## Summary

<img src="C:\Users\87932\AppData\Roaming\Typora\typora-user-images\image-20211122021235454.png" alt="image-20211122021235454" style="zoom:67%;" />

