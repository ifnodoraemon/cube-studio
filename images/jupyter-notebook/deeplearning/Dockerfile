FROM ccr.ccs.tencentyun.com/cube-studio/notebook:jupyter-ubuntu22.04

RUN apt-get update && apt install -y lsof
ENV TZ Asia/Shanghai
ENV DEBIAN_FRONTEND noninteractive

RUN mkdir -p /examples/ && git clone https://github.com/data-infra/cube-studio.git && cp -r cube-studio/aihub/deep-learning/* /examples/ && rm -rf cube-studio

# 基础工具
RUN apt install -y -f python3-opencv ffmpeg gcc automake autoconf libtool make ffmpeg build-essential
# 数据挖掘包
RUN pip install numpy pandas StatsModels Matplotlib Seaborn  sklearn wheel SciPy pyarrow Pillow PyML MDP Theano opencv-python plotly Bokeh Pydot tqdm gbdt xgboost lightgbm Eli5 \
    && rm -rf /tmp/* /var/tmp/* /root/.cache
# 深度学习包
RUN pip install tensorflow keras torch torchvision keras nltk spacy gensim fastai pytorch-lightning jax mxnet pytorch-ignite fasttext spacy tensorboard textblob \
    && rm -rf /tmp/* /var/tmp/* /root/.cache

# 安装插件
# RUN pip uninstall -y tensorboard && pip install tensorboard==2.10 jupyterlab-tensorboard-pro && jupyter labextension install jupyterlab_tensorboard_pro ; jupyter serverextension enable jupyterlab_tensorboard_pro --sys-prefix

# 拷贝examples
COPY examples/* /examples/

# 环境初始化配置
COPY init.sh /init.sh