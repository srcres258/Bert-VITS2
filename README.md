# Bert-VITS2 通过本地部署/colab在线训练和推理Bert-vits模型的简易教程

VITS2 Backbone with bert
### 严禁将此项目用于一切违反《中华人民共和国宪法》，《中华人民共和国刑法》，《中华人民共和国治安管理处罚法》和《中华人民共和国民法典》之用途。
### 严禁用于任何政治相关用途。
#### 基于b站up主团子是咸鱼的视频教程制作【Bert-Vits2 手把手本地部署录屏教程【已适配V1.1】】 https://www.bilibili.com/video/BV18N4y1Q7JK/?share_source=copy_web&vd_source=0850903c2c3f5ed7b220c9bda4e285f6
## References
## 原仓库链接：https://github.com/Stardust-minus/Bert-VITS2
## 基于原仓库有文件的修改
## 感谢所有贡献者作出的努力
## colab训练脚本
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/19fxpo-ZoL_ShEUeZIZi6Di-YioWrEyhR#scrollTo=0gQcIZ8RsOkn)
## 需要事先的准备工作：
+ 1.若干时长的高质量语音文本  
+ 2.音频切割工具slicer-gui 
+ 3.数据处理和标注工具，来自b站up主领航员未鸟【Bert-VITS2/VITS】更快更准确！自动标注一键包来啦】 https://www.bilibili.com/video/BV1dr4y1X7RL/?share_source=copy_web&vd_source=0850903c2c3f5ed7b220c9bda4e285f6
## 1.克隆仓库
+ !git clone https://github.com/fishaudio/Bert-VITS2
### 准备工作，数据集的准备
+ 1.原始数据音频必须是.wav格式，使用slicer-gui将文件切割为短于20s的音频
+ 2.按照【Bert-VITS2/VITS】更快更准确！自动标注一键包来啦】 https://www.bilibili.com/video/BV1dr4y1X7RL/?share_source=copy_web&vd_source=0850903c2c3f5ed7b220c9bda4e285f6教程处理数据
+ 3.将处理后的clean_barbara.list文件上传到filelists文件夹，并改名成【自己需要的名字】
+ 4.将preprocess_text文件中的名字改为【自己需要的名字】
+ 5.创建raw文件夹和它的子文件夹【自己需要的名字】，将处理后的音频上传到【自己需要的名字】文件夹
# 至此准备工作完成，开始训练

## 2.安装cuda，colab自带，建议重新安装一个11.8的版本
+ !pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
## 3.安装需要的依赖
+ %cd /content/Bert-VITS2/
+ !pip install -r requirements.txt
## 4.下载必要的模型到对应目录
+ hugging face不提供直链下载，使用二次分发下载模型
+ !wget -P bert/chinese-roberta-wwm-ext-large/ https://huggingface.co/hfl/chinese-roberta-wwm-ext-large/resolve/main/flax_model.msgpack
+ !wget -P bert/chinese-roberta-wwm-ext-large/ https://huggingface.co/hfl/chinese-roberta-wwm-ext-large/resolve/main/pytorch_model.bin
+ !wget -P bert/chinese-roberta-wwm-ext-large/ https://huggingface.co/hfl/chinese-roberta-wwm-ext-large/resolve/main/tf_model.h5
## 5.下载底模到对应文件夹
+ !wget -P logs/ztt/ https://huggingface.co/Erythrocyte/bert-vits2_base_model/resolve/main/DUR_0.pth
+ !wget -P logs/ztt/ https://huggingface.co/Erythrocyte/bert-vits2_base_model/resolve/main/D_0.pth
+ !wget -P logs/ztt/ https://huggingface.co/Erythrocyte/bert-vits2_base_model/resolve/main/G_0.pth
## 6.重采样
+ !python resample.py
## 7.执行preprocess_text.py
+ !python preprocess_text.py
## 8.执行!python bert_gen.py
+ !python bert_gen.py
## 9.开始训练
+ !python train_ms.py -m ztt -c configs/config.json
## 10.在线推理
+ !python webui.py











