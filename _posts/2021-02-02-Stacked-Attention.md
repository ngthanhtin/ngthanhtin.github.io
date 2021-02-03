---
layout: post
title: Stacked Attention for Visual Question Answering
subtitle: Attention
gh-repo: daattali/beautiful-jekyll
gh-badge: [settings]
tags: [vqa, attention]
comments: true

---
Hi, xin chào các bạn, hôm này mình sẽ giới thiệu cho các bạn mô hình <b>Stacked Attention</b> được dùng trong bài toán <b>Visual Question Answering (VQA)</b><br/>
Link paper: [Stacked Attention Networks for Image Question Answering (2016)](https://arxiv.org/abs/1511.02274)

Nội dung chính sẽ bao gồm các phần sau:<br/>
<a href="#1. Giới thiệu bài toàn Visual Question Answering">1. Giới thiệu bài toàn Visual Question Answering</a> <br/>
<a href="#2. Nguyên lý">2. Nguyên lý</a> <br/>
<a href="#3. Phương pháp">3. Phương pháp</a> <br/>
<a href="#4. Giải thuật">4. Giải thuật</a> <br/>
<a href="#5. Ứng dụng">5. Ứng dụng</a> <br/>
<a href="#6. Tham khảo">6. Tham khảo</a> <br/>

<section id="1. Giới thiệu bài toàn Visual Question Answering">
<b>1. Giới thiệu bài toàn Visual Question Answering</b>
</section>
Bài toán Visual Question Answering (VQA) là một trong những bài toán có sự kết hợp giữa Vision và Language. Đây là bài toán trả lời một câu hỏi dựa vào hình ảnh, mô hình vì thế phải học được sự liên hệ giữa hình ảnh và ngôn ngữ, từ đó đưa ra được câu trả lời phù hợp.
<p align="center">
  <img src="https://github.com/ngthanhtin/ngthanhtin.github.io/blob/master/_data/vqa/process.png?raw=true">
</p>

<section id="2. Nguyên lý">
<b>2. Nguyên lý</b>
</section>
Nguyên lý của bài toán đơn giản là dùng biểu diễn ngữ nghĩa của câu text để tìm vị trí của một vùng trong hình ảnh có liên quan tới câu trả lời.<br/>


<section id="3. Phương pháp">
<b>3. Phương pháp</b>
</section>
Bài báo đề xuất phương pháp Stacked Attention, đây là một phương pháp cho phép diễn dịch hình ảnh theo nhiều bước. Ví dụ cho câu hỏi và hình ảnh sau:<br/>
Câu hỏi: <b> What are sitting in the basket on a bicycle </b><br/>
Hình ảnh:
<p align="center">
  <img src="https://github.com/ngthanhtin/ngthanhtin.github.io/blob/master/_data/vqa/attention.png?raw=true">
</p>
Và ta sử dụng 2 lớp attention, thì lớp attention đầu tiên sẽ định vị những đối tượng như <b>basket, bicycle</b> sau đó ở những lớp attention tiếp theo sẽ dần dần loại bỏ những đối tượng không liên quan và cho ra đối tượng cần thiết.<br/>
<b>3.1 Image Model</b><br/>
Ở bài báo này, họ đã dùng mô hình VGG Net để lấy feature representation của image.<br/>
<p align="center">
  <img src="https://github.com/ngthanhtin/ngthanhtin.github.io/blob/master/_data/vqa/vgg.png?raw=true">
</p>

<b>3.2 Question Model</b><br/>
Đối với text presentation, ở bài báo họ sử dụng 2 cách: <b>(1) dùng lstm và sử dụng hidden để làm vector representation cho text</b> và <b>(2) sử dụng unigram để lấy vector presentation cho từng word, sau đó concatenate các vector này lại tạo thành vector representation cho text</b><br/>
Ở post này mình chỉ nói qua phương pháp (1).<br/>
<p align="center">
  <img src="https://github.com/ngthanhtin/ngthanhtin.github.io/blob/master/_data/vqa/lstm.png?raw=true">
</p>

<b>3.3 Stacked Attention Network</b><br/>

<section id="4. Giải thuật">
<b>4. Giải thuật</b>
</section>


<section id="5. Ứng dụng">
<b>5. Ứng dụng</b>
</section>
Hiện nay, các bài toán kết hợp vision và language đang là một hot trend trên thế giới, vì vậy càng ngày càng có nhiều mô hình giúp học được sự liên hệ giữa vision và language. Stacked Attention Network là một trong số đó, và nó có thể được áp dụng cho những bài toán có sự kết hợp giữa Vision và Language ví dụ như: <i>Medical Question Answering</i>, <i>Language Tracking</i>, <i>Visual Grounding</i>, <i>Image Captioning</i>, <i>Embodied Question Answering</i>, etc.<br/>

<section id="6. Tham khảo">
<b>6. Tham khảo</b>
</section>
Yang, Zichao, et al. "Stacked attention networks for image question answering." Proceedings of the IEEE conference on computer vision and pattern recognition. 2016.<br/>
