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

* 執行
```
!python ctc_tensorflow_example16000fin002.py
```


範例修改
* generate_audio_cache.py
* 將sample rate更改為16000
```
def get_script_arguments():
    args = ArgumentParser()
    args.add_argument('--audio_dir', required=True)
    args.add_argument('--output_dir', default='cache', type=ensure_dir)
    args.add_argument('--sample_rate', default=16000, type=int)
    args.add_argument('--speakers_sub_list', default='p225')  # example: p225,p226,p227
    return args.parse_args()
```

*  ctc_tensorflow_example16000fin002.py
*  更改sample rate為16000及其他參數

```
#路徑設定
modelpath = 'model'
modelname = 'ctc-5615'

sample_rate = 16000
# Some configs
num_features = 26  # log filter bank or MFCC features
# Accounting the 0th index +  space + blank label = 28 characters
num_classes = ord('z') - ord('a') + 1 + 1 + 1

# Hyper-parameters
num_epochs = 10000 #10000
num_hidden = 1024
batch_size = 16

num_examples = 1
num_batches_per_epoch = 10

#加入model存擋
with tf.Session(graph=graph) as session:

        tf.global_variables_initializer().run()
        
        saver = tf.train.Saver(max_to_keep=None)
        if not os.path.exists(modelpath):
            os.mkdir(modelpath)
        
        for curr_epoch in range(num_epochs):
            train_cost = train_ler = 0
            start = time.time()
            
            if ((curr_epoch + 1) % 1 == 0):
                save_path = saver.save(session, modelpath + '/' +modelname,global_step = curr_epoch + 1)
                print('save model to',save_path)
```

 測試
```
sample_rate = 16000
# Some configs
num_features = 26  # log filter bank or MFCC features
# Accounting the 0th index +  space + blank label = 28 characters
num_classes = ord('z') - ord('a') + 1 + 1 + 1

# Hyper-parameters
num_epochs = 1 #10000
num_hidden = 1024
batch_size = 346

num_examples = 1
num_batches_per_epoch = 1

# make sure the values match the ones in generate_audio_cache.py
audio = AudioReader(audio_dir='test',
                    cache_dir='cache_test',
                    sample_rate=sample_rate)
 ```

```
#還原model
 with tf.Session(graph=graph) as session:

        #tf.global_variables_initializer().run()
        
        saver = tf.train.Saver(max_to_keep=None)
        if os.path.exists('models/checkpoint'):
           saver.restore(session,'models/ctc-5615-1468')
        else:
            init = tf.global_variables_initializer()
            session.run(init)```

```


<h1>程式方塊圖與寫法</h1>

![image](https://github.com/MachineLearningNTUT/regression-109318083/blob/main/Diagram.jpg)

<h1>畫圖做結果分析</h1>

    
<h1> 討論預測值誤差很大的，是怎麼回事？ 如何改進？</h1> 
    
    
