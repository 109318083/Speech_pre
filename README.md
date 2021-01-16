[![Work in Repl.it](https://classroom.github.com/assets/work-in-replit-14baed9a392b3a25080506f3b7b6d57f295ec2978f6f33ec97e36a161684cbe9.svg)](https://classroom.github.com/online_ide?assignment_repo_id=3642470&assignment_repo_type=AssignmentRepo)


<h1>報告要包括</h1>

>做法說明

>程式方塊圖與寫法

>畫圖做結果分析

>討論預測值誤差很大的，是怎麼回事？

>如何改進？

<h1>做法說明</h1>

 訓練

* 本次用colab進行訓練,因為此範例用的是TF1.X的語法故先降版本

```jupyternotebook
!pip uninstall tensorflow
!pip install tensorflow==1.15 
!pip install tensorflow-gpu==1.15  
  ```
  + 進行目錄切換
```
%cd /home/tensorflow-ctc-speech-recognition-master
```
* 安裝colab所缺少的套件
```
!pip install python_speech_features fast_ctc_decode
```

  執行
```
!python ctc_tensorflow_example16000fin002.py
```

* 範例修改




<h1>程式方塊圖與寫法</h1>

![image](https://github.com/MachineLearningNTUT/regression-109318083/blob/main/Diagram.jpg)

<h1>畫圖做結果分析</h1>

    
<h1> 討論預測值誤差很大的，是怎麼回事？ 如何改進？</h1> 
    
    
