# CNN_Denoising <br>

　　地震勘探数据采集过程中多方面影响，使得到的地震数据都是含有有效信号和噪声的混波记录。 <br>
噪声的存在使得有效的地震数据很难被识别，因此在实际应用中去除噪声干扰是地震数据处理流程　 <br>
中的重要步骤。为解决在去噪的过程中需要人为设定去噪阈值，实现起来较为复杂，效率较低等问  <br>
题，提供一种深度学习模型训练方法和地震数据去噪方法以实现高效、智能化地进行地震数据去噪 <br>
的效果。

### 去噪模型 <br>
*  地震数据去噪模型以卷积自动编码器为原型 <br>
*  将输入样本压缩到隐层，然后解压，在输出端重建样本 <br>
*  通过网络学习将冗余信息去掉，将有用信息输入到隐层中，通过隐层的特征信息重建得到无噪声的图片 <br> 
#### 网络结构图： <br>
　　　　　　　　　　　　　　　![image](https://github.com/lulu-313/DNN_Denoising/blob/master/image/%E7%BD%91%E7%BB%9C%E7%BB%93%E6%9E%84%E5%9B%BE.png)<br> 

　　去噪模型总共10层，从上到下分别是输入层、卷积层、最大池化层、卷积层、最大池化层、卷积层、上采样层、 <br>
卷积层、上采样层和卷积层。其中第2层、第3层、第4层和第5层为编码器，第6层、第7层、第8层、第9层和第10 <br>
层为解码器。 <br>
第1层为输入层，输入维度为60x60x1;  <br>
第2层为一个卷积层，卷积核大小为3x3,卷积核个数为32，使用的激活函数为relu，输出大小为60x60x32；<br>
第3层是最大池化层，池化核大小为2 x 2，stride默认为1，padding为same，池化后的大小为30x30x32；<br>
第4层是与第2层相同的卷积层，经过第4层的卷积层后，图像变为30x30x32； <br>
第5层是与第3层相同的池化层，经过第5层的池化层之后图片变为15x15x32； <br>

第6层为反卷基层，卷积核大小为3x3,卷积核个数为32，使用的激活函数为relu，15x15x32； <br>
第7层是一个上采样层，目的是恢复原图片的大小，经过第7层上采样层之后，图片变为30x30x32； <br>
同理经过第8层卷积层和第9层上采样层之后，图片变为60 x 60 x 32； <br>
第10层也是一个卷积层，其与其他层不同的部分是卷积核数目为1，激活函数为sigmoid，恢复图片大小为60x60x1。 <br>
以上便是去噪模型的网络结构。 <br>

#### 卷积特征提取过程： <br>
![image](https://github.com/lulu-313/DNN_Denoising/blob/master/image/%E5%88%87%E7%89%87.png)<br> 


 
