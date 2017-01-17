
2016年 12月 13日 星期二 10:19:33 CST

1. 安装 pdftk

* 将多个 pdf 合并成一个

`>* pdftk 1.pdf 2.pdf 3.pdf cat output 123.pdf`

2. 安装 pfdimages

* 从 pdf 提取图像
`pfdimages example.pdf exampleimage`

* -j 选项将图像保存为 JPG 格式
`pfdimages -j example.pdf exampleimage`

* 指定起始和结束页，例如第 3 到第 7 页
` pfdimages -f 3 -l 7 example.pdf exampleimage`

3. 安装 imagemagick 

`sudo aptitude install imagemagick`

* 转换为图片
`convert doc.pdf doc.jpeg`

 通过“resize 1800”参数即可设置输出图片的宽度为1800像素
`convert -verbose \
    -colorspace RGB \
    -resize 1800 \ 
	-interlace none \
	-density 300 \
	-quality 100 \
	XXX.pdf XXX.jpg`
	
`>* convert -verbose -resize 750 -interlace none -density 800 -quality 100 1.pdf 800.jpg`

	


