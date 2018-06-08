I uploaded training dataset(4000 images) and test dataset(1000 images).
Each dataset consists of 3 gz files(image, label-digit, label-color) and has the same format as the ordinary MNIST dataset.

When you use the dataset

Unzip the datasets.
Each file is a byte code. So you have to change it to integer. Here is an example of decoding the datasets.

import numpy as np
from struct import *

images = open('test-images-ubyte', 'rb')
digits = open('test-label-digit-ubyte', 'rb')
colors = open('test-label-color-ubyte', 'rb')

for i in range(4000):
    image_byte = images.read(28 * 28 * 3)
    digit_byte = digits.read(1)
    color_byte = colors.read(3)

    image = np.reshape(unpack(len(image_byte) * 'B', image_byte), [28, 28, 3])
    digit = unpack(len(digit_byte) * 'B', digit_byte)
    color = unpack(len(color_byte) * 'B', color_byte)
Then, you can get an image and the corresponding digit and color,
Note that digit is not a one-hot vector, but a scalar value.

If there is any problem with the datasets, feel free to contact me.
Thanks.
