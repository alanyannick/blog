---
title: Hello World
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)

eg.prototxt
```
name: "CaffeNet"
layers {
  name: "data"
  type: DATA
  top: "data_age"
  top: "label_age"
  data_param {
    source: "age_train_leveldb"
    mean_file: "mean.binaryproto"
    batch_size: 50
    crop_size: 227
    mirror: true
  }
  include: { phase: TRAIN }
}
layers {
  name: "data"
  type: DATA
  top: "data_age"
  top: "label_age"
  data_param {
    source: "age_val_leveldb"
    mean_file: "mean.binaryproto"
    batch_size: 50
    crop_size: 227
    mirror: false
  }
  include: { phase: TEST }
}
layers {
  name: "data"
  type: DATA
  top: "data_gender"
  top: "label_gender"
  data_param {
    source: "gender_train_leveldb"
    mean_file: "mean.binaryproto"
    batch_size: 50
    crop_size: 227
    mirror: true
  }
  include: { phase: TRAIN }
}
layers {
  name: "data"
  type: DATA
  top: "data_gender"
  top: "label_gender"
  data_param {
    source: "gender_val_leveldb"
    mean_file: "mean.binaryproto"
    batch_size: 50
    crop_size: 227
    mirror: false
  }
  include: { phase: TEST }
}
layers {
  name: "conv1"
  type: CONVOLUTION
  bottom: "data_age"
  bottom: "data_gender"
  top: "conv1_age"
  top: "conv1_gender"
  blobs_lr: 1
  blobs_lr: 2
  weight_decay: 1
  weight_decay: 0
  convolution_param {
    num_output: 96
    kernel_size: 11
    stride: 4
    weight_filler {
      type: "gaussian"
      std: 0.01
    }
    bias_filler {
      type: "constant"
      value: 0
    }
  }
}
layers {
  name: "relu1_age"
  type: RELU
  bottom: "conv1_age"
  top: "conv1_age"
}
layers {
  name: "relu1_gender"
  type: RELU
  bottom: "conv1_gender"
  top: "conv1_gender"
}
layers {
  name: "pool1_age"
  type: POOLING
  bottom: "conv1_age"
  top: "pool1_age"
  pooling_param {
    pool: MAX
    kernel_size: 3
    stride: 2
  }
}
layers {
  name: "pool1_gender"
  type: POOLING
  bottom: "conv1_gender"
  top: "pool1_gender"
  pooling_param {
    pool: MAX
    kernel_size: 3
    stride: 2
  }
}
layers {
  name: "norm1_age"
  type: LRN
  bottom: "pool1_age"
  top: "norm1_age"
  lrn_param {
    local_size: 5
    alpha: 0.0001
    beta: 0.75
  }
}
layers {
  name: "norm1_gender"
  type: LRN
  bottom: "pool1_gender"
  top: "norm1_gender"
  lrn_param {
    local_size: 5
    alpha: 0.0001
    beta: 0.75
  }
}
layers {
  name: "conv2"
  type: CONVOLUTION
  bottom: "norm1_age"
  bottom: "norm1_gender"
  top: "conv2_age"
  top: "conv2_gender"
  blobs_lr: 1
  blobs_lr: 2
  weight_decay: 1
  weight_decay: 0
  convolution_param {
    num_output: 256
    pad: 2
    kernel_size: 5
    group: 2
    weight_filler {
      type: "gaussian"
      std: 0.01
    }
    bias_filler {
      type: "constant"
      value: 1
    }
  }
}
layers {
  name: "relu2_age"
  type: RELU
  bottom: "conv2_age"
  top: "conv2_age"
}
layers {
  name: "relu2_gender"
  type: RELU
  bottom: "conv2_gender"
  top: "conv2_gender"
}
layers {
  name: "pool2_age"
  type: POOLING
  bottom: "conv2_age"
  top: "pool2_age"
  pooling_param {
    pool: MAX
    kernel_size: 3
    stride: 2
  }
}
layers {
  name: "pool2_gender"
  type: POOLING
  bottom: "conv2_gender"
  top: "pool2_gender"
  pooling_param {
    pool: MAX
    kernel_size: 3
    stride: 2
  }
}
layers {
  name: "norm2_age"
  type: LRN
  bottom: "pool2_age"
  top: "norm2_age"
  lrn_param {
    local_size: 5
    alpha: 0.0001
    beta: 0.75
  }
}
layers {
  name: "norm2_gender"
  type: LRN
  bottom: "pool2_gender"
  top: "norm2_gender"
  lrn_param {
    local_size: 5
    alpha: 0.0001
    beta: 0.75
  }
}
layers {
  name: "conv3"
  type: CONVOLUTION
  bottom: "norm2_age"
  bottom: "norm2_gender"
  top: "conv3_age"
  top: "conv3_gender"
  blobs_lr: 1
  blobs_lr: 2
  weight_decay: 1
  weight_decay: 0
  convolution_param {
    num_output: 384
    pad: 1
    kernel_size: 3
    weight_filler {
      type: "gaussian"
      std: 0.01
    }
    bias_filler {
      type: "constant"
      value: 0
    }
  }
}
layers {
  name: "relu3_age"
  type: RELU
  bottom: "conv3_age"
  top: "conv3_age"
}
layers {
  name: "relu3_gender"
  type: RELU
  bottom: "conv3_gender"
  top: "conv3_gender"
}
layers {
  name: "conv4"
  type: CONVOLUTION
  bottom: "conv3_age"
  bottom: "conv3_gender"
  top: "conv4_age"
  top: "conv4_gender"
  blobs_lr: 1
  blobs_lr: 2
  weight_decay: 1
  weight_decay: 0
  convolution_param {
    num_output: 384
    pad: 1
    kernel_size: 3
    group: 2
    weight_filler {
      type: "gaussian"
      std: 0.01
    }
    bias_filler {
      type: "constant"
      value: 1
    }
  }
}
layers {
  name: "relu4_age"
  type: RELU
  bottom: "conv4_age"
  top: "conv4_age"
}
layers {
  name: "relu4_gender"
  type: RELU
  bottom: "conv4_gender"
  top: "conv4_gender"
}
layers {
  name: "conv5"
  type: CONVOLUTION
  bottom: "conv4_age"
  bottom: "conv4_gender"
  top: "conv5_age"
  top: "conv5_gender"
  blobs_lr: 1
  blobs_lr: 2
  weight_decay: 1
  weight_decay: 0
  convolution_param {
    num_output: 256
    pad: 1
    kernel_size: 3
    group: 2
    weight_filler {
      type: "gaussian"
      std: 0.01
    }
    bias_filler {
      type: "constant"
      value: 1
    }
  }
}
layers {
  name: "relu5_age"
  type: RELU
  bottom: "conv5_age"
  top: "conv5_age"
}
layers {
  name: "relu5_gender"
  type: RELU
  bottom: "conv5_gender"
  top: "conv5_gender"
}
layers {
  name: "pool5_age"
  type: POOLING
  bottom: "conv5_age"
  top: "pool5_age"
  pooling_param {
    pool: MAX
    kernel_size: 3
    stride: 2
  }
}
layers {
  name: "pool5_gender"
  type: POOLING
  bottom: "conv5_gender"
  top: "pool5_gender"
  pooling_param {
    pool: MAX
    kernel_size: 3
    stride: 2
  }
}
layers {
  name: "fc6_age"
  type: INNER_PRODUCT
  bottom: "pool5_age"
  top: "fc6_age"
  blobs_lr: 1
  blobs_lr: 2
  weight_decay: 1
  weight_decay: 0
  inner_product_param {
    num_output: 4096
    weight_filler {
      type: "gaussian"
      std: 0.005
    }
    bias_filler {
      type: "constant"
      value: 1
    }
  }
}
layers {
  name: "fc6_gender"
  type: INNER_PRODUCT
  bottom: "pool5_gender"
  top: "fc6_gender"
  blobs_lr: 1
  blobs_lr: 2
  weight_decay: 1
  weight_decay: 0
  inner_product_param {
    num_output: 4096
    weight_filler {
      type: "gaussian"
      std: 0.005
    }
    bias_filler {
      type: "constant"
      value: 1
    }
  }
}
layers {
  name: "relu6_age"
  type: RELU
  bottom: "fc6_age"
  top: "fc6_age"
}
layers {
  name: "relu6_gender"
  type: RELU
  bottom: "fc6_age"
  top: "fc6_age"
}
layers {
  name: "drop6_age"
  type: DROPOUT
  bottom: "fc6_age"
  top: "fc6_age"
  dropout_param {
    dropout_ratio: 0.5
  }
}
layers {
  name: "drop6_gender"
  type: DROPOUT
  bottom: "fc6_age"
  top: "fc6_age"
  dropout_param {
    dropout_ratio: 0.5
  }
}
layers {
  name: "fc7_age"
  type: INNER_PRODUCT
  bottom: "fc6_age"
  top: "fc7_age"
  # Note that blobs_lr can be set to 0 to disable any fine-tuning of this, and any other, layer
  blobs_lr: 1
  blobs_lr: 2
  weight_decay: 1
  weight_decay: 0
  inner_product_param {
    num_output: 4096
    weight_filler {
      type: "gaussian"
      std: 0.005
    }
    bias_filler {
      type: "constant"
      value: 1
    }
  }
}
layers {
  name: "fc7_gender"
  type: INNER_PRODUCT
  bottom: "fc6_gender"
  top: "fc7_gender"
  # Note that blobs_lr can be set to 0 to disable any fine-tuning of this, and any other, layer
  blobs_lr: 1
  blobs_lr: 2
  weight_decay: 1
  weight_decay: 0
  inner_product_param {
    num_output: 4096
    weight_filler {
      type: "gaussian"
      std: 0.005
    }
    bias_filler {
      type: "constant"
      value: 1
    }
  }
}
layers {
  name: "relu7_age"
  type: RELU
  bottom: "fc7_age"
  top: "fc7_age"
}
layers {
  name: "relu7_gender"
  type: RELU
  bottom: "fc7_gender"
  top: "fc7_gender"
}
layers {
  name: "drop7_age"
  type: DROPOUT
  bottom: "fc7_age"
  top: "fc7_age"
  dropout_param {
    dropout_ratio: 0.5
  }
}
layers {
  name: "drop7_gender"
  type: DROPOUT
  bottom: "fc7_gender"
  top: "fc7_gender"
  dropout_param {
    dropout_ratio: 0.5
  }
}
layers {
  name: "fc8_age"
  type: INNER_PRODUCT
  bottom: "fc7_age"
  top: "fc8_age"
  # blobs_lr is set to higher than for other layers, because this layer is starting from random while the others are already trained
  blobs_lr: 10
  blobs_lr: 20
  weight_decay: 1
  weight_decay: 0
  inner_product_param {
    num_output: 8
    weight_filler {
      type: "gaussian"
      std: 0.01
    }
    bias_filler {
      type: "constant"
      value: 0
    }
  }
}
layers {
  name: "fc8_gender"
  type: INNER_PRODUCT
  bottom: "fc7_gender"
  top: "fc8_gender"
  # blobs_lr is set to higher than for other layers, because this layer is starting from random while the others are already trained
  blobs_lr: 10
  blobs_lr: 20
  weight_decay: 1
  weight_decay: 0
  inner_product_param {
    num_output: 2
    weight_filler {
      type: "gaussian"
      std: 0.01
    }
    bias_filler {
      type: "constant"
      value: 0
    }
  }
}
layers {
  name: "loss_age"
  type: SOFTMAX_LOSS
  bottom: "fc8_age"
  bottom: "label_age"
}
layers {
  name: "loss_gender"
  type: SOFTMAX_LOSS
  bottom: "fc8_gender"
  bottom: "label_gender"
}
layers {
  name: "accuracy_age"
  type: ACCURACY
  bottom: "fc8_age"
  bottom: "label_age"
  top: "accuracy_age"
  include: { phase: TEST }
}
layers {
  name: "accuracy_gender"
  type: ACCURACY
  bottom: "fc8_gender"
  bottom: "label_gender"
  top: "accuracy_gender"
  include: { phase: TEST }
}
```