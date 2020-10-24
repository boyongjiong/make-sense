[![Build Status](https://travis-ci.org/SkalskiP/make-sense.svg?branch=develop)](https://travis-ci.org/SkalskiP/make-sense)
![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/SkalskiP/make-sense?include_prereleases)
[![Gitter](https://badges.gitter.im/make-sense-ai/community.svg)](https://gitter.im/make-sense-ai/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

<h1 align="center">makesense.ai</h1>

<p align="center"> 
  <img width="600" src=".//public/ico/main-image-dark_alter.png" alt="Logo">
</p>

## 简介

[makesense.ai][1] 是一款免费的图片标注的在线工具。多亏使用浏览器，它不需要任何复杂的安装 - 仅通过访问网站就可以了。在什么样的操作系统上运行也不重要 - 我们尽力坐到了真正的跨平台。它非常适合小型电脑上视觉深度学习项目，使准备数据集的过程更加简单和快捷。准备好的标签可以以多种支持的格式下载。该项目是用 TypeScript 编写的，基于 React/Redux 二人组。

## 格言

> For AI to be free we need not just Open Source, but also a strong Open Data movement.

Andrew Ng

## 先睹为快

<p align="center"> 
  <img width="1000" src=".//examples/demo-base.gif" alt="alfa-demo">
</p>

**Figure 1.** 应用程序的基础功能-不包括 AI

## 高级 AI 功能

[makesense.ai][1] 致力于大幅减少我们在图片标注上花费的时间。为了实现这一目标，我们将使用很多不同的人工智能模型，这些模型将能够给你提供建议，以及自动完成重复性和乏味的活动。

* [SSD 模型][8] 在[COCO 数据集][9]上进行预训练，它将为你做一些在照片画 bboxes (bbox是每个region矩形框的位置信息。)的工作，并且还（在有些情况下）建议一个标签。
* [PoseNet 模型][11] 是一个视觉模型，可以通过估计身体关键关节的位置来推定推定或视频中一个人的姿势。

在未来，我们还计划添加，照片分类、检测人脸特征以及整个脸的模型。驱动我们 AI 功能的引擎是 [TensorFlow.js][10] - 最流行的神经网络训练框架的 JS 版本。这种选择不仅可以让我们加快你的工作速度，还可以关心你的数据隐私，因为与其它商业和开源工具不同，你的照片不必传输到服务器。这一次，AI 来到了你的设备上！

<p align="center"> 
  <img width="1000" src=".//examples/demo-ssd.gif" alt="ai-demo">
</p>

**Figure 2.** SSD 模型 - 允许你检测多个对象，加快 bbox 标签过程

<p align="center"> 
  <img width="1000" src=".//examples/demo-posenet.gif" alt="ai-demo">
</p>

**Figure 3.** PoseNet 模型 - 允许你检测照片中人们的姿势，在某些情况下自动进行点标签

## 在本地创建项目

```bash
# clone repository
git clone https://github.com/SkalskiP/make-sense.git

# navigate to main dir
cd make-sense

# install dependencies
npm install

# serve with hot reload at localhost:3000
npm start
```
为了确保应用程序在本地的正常功能，需要 npm`6.x.x` 和 node.js `v11.x.x`版本。关于这个问题的更多信息可以在[#16][4]中找到。

## 使用 Docker 设置项目

```bash
# Build Docker Image
docker build -t make_sense docker/

# Run Docker Image as Service
docker run -dit -p 3000:3000 --restart=always --name=make_sense make_sense

# Get Docker Container IP
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' make_sense
# Go to `<DOCKER_CONTAINER_IP>:3000`

# Get Docker Container Logs
docker logs make_sense
```

## 支持的键盘快捷键

| Functionality                      | Context  | Mac | Windows / Linux  |
|:-----------------------------------|:--------:|:---:|:----------------:|
| Polygon autocomplete               | Editor   | <kbd>Enter</kbd> | <kbd>Enter</kbd> |
| Cancel polygon drawing             | Editor   | <kbd>Escape</kbd> | <kbd>Escape</kbd> |
| Delete currently selected label    | Editor   | <kbd>Backspace</kbd> | <kbd>Delete</kbd> |
| Load previous image                | Editor   | <kbd>⌥</kbd> + <kbd>Left</kbd> | <kbd>Ctrl</kbd> + <kbd>Left</kbd> |
| Load next image                    | Editor   | <kbd>⌥</kbd> + <kbd>Right</kbd> | <kbd>Ctrl</kbd> + <kbd>Right</kbd> |
| Zoom in                            | Editor   | <kbd>⌥</kbd> + <kbd>+</kbd> | <kbd>Ctrl</kbd> + <kbd>+</kbd> |
| Zoom out                           | Editor   | <kbd>⌥</kbd> + <kbd>-</kbd> | <kbd>Ctrl</kbd> + <kbd>-</kbd> |
| Move image                         | Editor   | <kbd>Up</kbd> / <kbd>Down</kbd> / <kbd>Left</kbd> / <kbd>Right</kbd> | <kbd>Up</kbd> / <kbd>Down</kbd> / <kbd>Left</kbd> / <kbd>Right</kbd> |
| Exit popup                         | Popup    | <kbd>Escape</kbd> | <kbd>Escape</kbd> |

**Table 1.** Supported keyboard shortcuts

## 支持的导出格式

|               | CSV | YOLO | VOC XML | VGG JSON | COCO JSON | PIXEL MASK |
|:-------------:|:---:|:----:|:-------:|:--------:|:---------:|:----------:|
| **Point**     | ✓   | ✗    | ☐       | ☐        | ☐         | ✗          |
| **Line**      | ✓   | ✗    | ✗       | ✗        | ✗         | ✗          |
| **Rect**      | ✓   | ✓    | ✓       | ☐        | ☐         | ✗          |
| **Polygon**   | ☐   | ✗    | ☐       | ✓        | ✓         | ☐          |
| **Label**     | ✓   | ✗    | ✗       | ✗        | ✗         | ✗          |

**Table 2.** The matrix of supported labels export formats, where:
* ✓ - 支持的格式
* ☐ - 尚未支持的格式
* ✗ - 对于给定的标签类型，格式没有意义

你可以在我们的[Wiki][7]上找到导出文件的例子以及描述和模式。

## 支持的导入格式

|               | CSV | YOLO | VOC XML | VGG JSON | COCO JSON | PIXEL MASK |
|:-------------:|:---:|:----:|:-------:|:--------:|:---------:|:----------:|
| **Point**     | ☐   | ✗    | ☐       | ☐        | ☐         | ✗          |
| **Line**      | ☐   | ✗    | ✗       | ✗        | ✗         | ✗          |
| **Rect**      | ☐   | ✓    | ☐       | ☐        | ✓         | ✗          |
| **Polygon**   | ☐   | ✗    | ☐       | ☐        | ✓         | ☐          |
| **Label**     | ☐   | ✗    | ✗       | ✗        | ✗         | ✗          |

**Table 3.** The matrix of supported labels import formats

## 隐私保护

我们不存储您的图片，因为我们不会把他们发送到任何地方。

## 开发规划

我们的程序正在积极开发中。请在我们的[Wiki][6]上查看我们的近期计划。如果你有新功能的想法，请在[Twitter][3]或[Gitter][5]上联系我们，或者创建一个issue，在哪里你可以描述你的概念。同事，看看我们在未来为您规划了那些改进。

## 指南

如果你刚刚开始深度学习的冒险，并希望在这条路上学习了创造一些很酷的东西，[makesense.ai][1]可以帮助你。利用我们的边界框标签功能来准备一个数据集，并使用它来训练你的 第一个最先进的对象检测模型。按照[说明][12]和[示例][13]，但最重要的是，解放你的创造力。

<p align="center"> 
    <img width="800" src=".//examples/object_detection_basketball.gif" alt="Object detection tutorial">
</p>

**Figure 4.** 基于<a href="https://research.google.com/youtube8m/">YouTube-8M</a>数据集，检测球员在篮球场上的移动。

## 贡献

欢迎提交 [issues](https://github.com/SkalskiP/make-sense/issues) 或 [pull requests](https://github.com/SkalskiP/make-sense/pulls).  

## 引用

```
@MISC{make-sense,
   author = {Piotr Skalski},
   title = {{Make Sense}},
   howpublished = "\url{https://github.com/SkalskiP/make-sense/}",
   year = {2019},
}
```

## License

This project is licensed under the GPL-3.0 License - see the [LICENSE][2] file for details

Copyright (c) 2019-present, Piotr Skalski

[1]: http://makesense.ai
[2]: ./LICENSE
[3]: https://twitter.com/PiotrSkalski92
[4]: https://github.com/SkalskiP/make-sense/issues/16
[5]: https://gitter.im/make-sense-ai/community?utm_source=share-link&utm_medium=link&utm_campaign=share-link
[6]: https://github.com/SkalskiP/make-sense/wiki/Road-Map
[7]: https://github.com/SkalskiP/make-sense/wiki/Supported-Output-Formats
[8]: https://arxiv.org/abs/1512.02325
[9]: http://cocodataset.org
[10]: https://www.tensorflow.org/js
[11]: https://www.tensorflow.org/lite/models/pose_estimation/overview
[12]: https://towardsdatascience.com/chess-rolls-or-basketball-lets-create-a-custom-object-detection-model-ef53028eac7d
[13]: https://github.com/SkalskiP/ILearnDeepLearning.py/tree/master/02_data_science_toolkit/02_yolo_object_detection
