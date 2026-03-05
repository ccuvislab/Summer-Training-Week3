# Week 3 — Detectron2 Installation & Version Downgrade / Detectron2 安裝與降版

> **[English](#english) | [中文](#中文)**

---

<a id="english"></a>

## English

### Learning Objectives

* Learn how to download and use an older version of Detectron2 (v0.5) from GitHub.
* Handle PyTorch version and compatibility issues by creating a Conda virtual environment.
* Acquire the ability to perform model training and inference.
* Learn to modify framework configuration files (config files) for customization.
* Learn how to register datasets in Detectron2.

### Assignment

#### 1. Environment Setup and Configuration

* Create a Conda virtual environment.
* Install and configure the appropriate PyTorch version.
* Clone Detectron2 from GitHub.
* Install the required dependencies (detectron2==0.5) and verify the environment works correctly.
```bash
pip install git+https://github.com/facebookresearch/detectron2.git@v0.5
```

#### 2. Model Training and Inference

* Register and use the Cityscapes and Foggy_Cityscapes datasets to train a model.
* Run train_net.py to ensure the training process runs correctly, and save the training results.
* Write an inference script to perform object detection on images in the dataset (test set only) using the trained model.

#### 3. Modify and Customize Configuration Files

* Learn the structure of configuration files, and adjust training parameters such as number of iterations, batch size, etc.
* Verify that the modified configuration files are successfully applied to model training and inference.

### Submission Requirements

* Complete documentation of environment setup steps.
* Screenshots of model training and inference results.
* Problems encountered and how they were resolved.
* Modified config files, with explanations of the purpose and results of the modifications.

Please fork this repository first — go to the [GitHub Assignment](https://github.com/ccuvislab/Summer-Training-Week3) and click Fork to copy it to your own GitHub account. All subsequent clone, commit, push operations should be done in your own repository.
* Apart from pushing the config files modified for the Foggy dataset and the inference script, please rewrite your documentation and results into a new README.md file.

### Important Notes

1. There is already a train_net.py and a Cityscapes config file (using ResNet50 as backbone). Please first try to complete model training with the Cityscapes dataset (no config modification needed), then use the Foggy dataset and modify some config parameters to complete training.
```bash
python train_net.py --config-file ./configs/city_resnet50.yaml --num-gpus 1 SOLVER.IMS_PER_BATCH 2 SOLVER.BASE_LR 0.0025
```
2. Environment setup issues vary from person to person. For example, when testing with an RTX 4060 Ti, this GPU does not seem to support PyTorch versions below 2.1.0. Please choose an appropriate Python version when setting up the environment:
My environment: Python (3.8.20), PyTorch (2.1.0), CUDA 11.8.
First create the Conda environment, then **install packages inside the environment** for proper environment management.
```bash
conda create -n myenv python=3.8.20
conda activate myenv
```
You can find the desired installation commands on the [PyTorch website](https://pytorch.org/get-started/previous-versions/) (based on the environment settings above).
There is no restriction on which version to use — **as long as it is supported and runs properly**.
```bash
conda install pytorch==2.1.0 torchvision==0.16.0 torchaudio==2.1.0 pytorch-cuda=11.8 -c pytorch -c nvidia
```
Additionally, there are some minor issues during environment setup. For example, installing PyTorch (2.1.0) also installs Pillow (10.4.0), but older versions of Detectron2 do not support newer Pillow versions, so a downgrade is needed:
```bash
pip uninstall pillow
pip install pillow==9.0.1
```
3. Before installing the Detectron2 package, you also need to set up the build environment (gcc), otherwise the installation will fail. See the [Detectron2 Installation Guide](https://github.com/facebookresearch/detectron2/blob/main/INSTALL.md) for details.
4. The dataset can be found on the NAS at VIS_Lab/VIS_Lab共用(ALL)/99_Others/dataset/MSDAOD_dataset. Also, make sure the path is correct when registering the dataset.

### References

1. Detectron2 Official Tutorial: [Getting Started with Detectron2](https://detectron2.readthedocs.io/en/latest/)
2. When using TWCC, refer to the [Container Image Information](https://man.twcc.ai/@twccdocs/ccs-concept-image-main-zh/%2F%40twccdocs%2Fccs-concept-image-pytorch-zh)

---

<a id="中文"></a>

## 中文

### 學習目標

* 學習如何從 GitHub 下載並使用稍舊版 Detectron2 (v0.5)。
* 透過使用 Conda 建立虛擬環境，處理 PyTorch 版本與相容性問題。
* 具備進行模型訓練（training）與推論（inference）的能力。
* 學會修改框架設定檔（config files）以進行客製化調整。
* 學會如何在Detectron2上註冊資料集

### 作業內容

#### 1. 環境安裝與配置

* 建立 Conda 虛擬環境。
* 安裝並設定 PyTorch 版本。
* 從 GitHub clone Detectron2。
* 安裝所需相關依賴套件(detectron2==0.5)並確認環境運作正常。
```bash
pip install git+https://github.com/facebookresearch/detectron2.git@v0.5
```

#### 2. 模型訓練與推論

* 註冊與使用Cityscapes、Foggy_Cityscapes資料集訓練模型
* 執行train_net.py，確保訓練流程正常運行，並儲存訓練結果。
* 撰寫 inference 腳本，利用訓練好的模型對資料集(僅測試集)內圖片進行物件偵測。

#### 3. 修改並客製化設定檔

* 學習設定檔結構，調整訓練參數，如iteration數量、batch size等。
* 驗證修改後的設定檔是否成功作用於模型訓練與推論。

### 繳交內容

* 完整的環境安裝步驟說明。
* 模型訓練與推論結果截圖。
* 遇到的問題與如何解決。
* 修改後的 config 檔案，並說明修改的目的與成果。

請先Fork作業repository，到[Github作業](https://github.com/ccuvislab/Summer-Training-Week3)點選Fork到自己的github帳號內，後續clone,commit,push等都在自己的repository內進行。
* 除為了Foggy資料集修改的config檔案與inference檔案push上去外，說明與結果請改寫成一份新的README.md檔案

### 注意事項

1. 目前已經有train_net.py與Cityscapes的config檔(使用resnet50作為backbone)，請先試著使用Cityscapes資料集完成模型訓練(不需要修改config)，後續再使用Foggy資料集並修改一些config參數完成訓練
```bash
python train_net.py --config-file ./configs/city_resnet50.yaml --num-gpus 1 SOLVER.IMS_PER_BATCH 2 SOLVER.BASE_LR 0.0025
```
2. 針對環境安裝問題每個人大不相同，以我測試RTX 4060 Ti為例，這顆GPU似乎不支援pytorch 2.1.0以下版本，建立環境時請選擇適當的python版本：
我的環境為python(3.8.20),pytorch(2.1.0),CUDA 11.8
先使用conda建立好環境，之後「請在環境內安裝套件」以便做好環境控管
```bash
conda create -n myenv python=3.8.20
conda activate myenv
```
可以從[Pytorch網站](https://pytorch.org/get-started/previous-versions/)找到想要的安裝環境指令(依上述我想要的環境設定)
在選擇版本時並不限於哪種版本，「只要支援且能跑就好」
```bash
conda install pytorch==2.1.0 torchvision==0.16.0 torchaudio==2.1.0 pytorch-cuda=11.8 -c pytorch -c nvidia
```
另外我測試環境時同樣也有些小問題需要處理，像是安裝pytorch(2.1.0)時會順便安裝Pillow(10.4.0)，但在舊版detectron2中並不支援太新的Pillow套件，因此需要額外做降版
```bash
pip uninstall pillow
pip install pillow==9.0.1
```
3. 下載detectron2套件前同樣需要先準備好環境(gcc)，否則無法順利安裝在環境上，詳細說明可以[detectron2安裝說明](https://github.com/facebookresearch/detectron2/blob/main/INSTALL.md)查看
4. 資料集可以從NAS上的VIS_Lab/VIS_Lab共用(ALL)/99_Others/dataset/MSDAOD_dataset中找到，另外註冊資料集時也請確保路徑是正確的

### 參考連結

1. Detectron2官方教程：[Detectron2 入門](https://detectron2.readthedocs.io/en/latest/)
2. 使用TWCC時可參考的[映象檔資訊](https://man.twcc.ai/@twccdocs/ccs-concept-image-main-zh/%2F%40twccdocs%2Fccs-concept-image-pytorch-zh)
