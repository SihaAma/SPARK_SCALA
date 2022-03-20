What does this program do? 

create a Spark ML transformer,which will return a histogram for a given image.
Input data – image in binary format(Array[Byte]type)
Output – histogram for the image(Array[Int] type)

Spark image data source is used to load image files from a directory, it can load compressed image (jpeg, png, etc.) into raw image representation via ImageIO in Java library. 
The loaded DataFrame has one StructType column: “image”, containing image data stored as image schema. 
The schema of the image column is:

origin: StringType (represents the file path of the image)
height: IntegerType (height of the image)
width: IntegerType (width of the image)
nChannels: IntegerType (number of image channels)
mode: IntegerType (OpenCV-compatible type)
data: BinaryType (Image bytes in OpenCV-compatible order: row-wise BGR in most cases)


HistogramTransform and HistogramTransformModel aim to help convert image DataFrame
into another DataFrame with image histogram


The histogram is represented by an int array of 256 elements.
Each element gives the number of pixels in the image of the value equal to the index of the element.

HistogramTransform Compute a histogram using the provided buckets.

the bucket is a number, it will generate buckets which are evenly spaced between the minimum and maximum of the RDD.
For example, if the min value is 0 and the max is 100, given buckets as 2, the resulting buckets will be [0,50) [50,100]. 

The schema of the Result transform
|-- image: struct (nullable = true)
|    |-- origin: string (nullable = true)
|    |-- height: integer (nullable = true)
|    |-- width: integer (nullable = true)
|    |-- nChannels: integer (nullable = true)
|    |-- mode: integer (nullable = true)
|    |-- data: binary (nullable = true)
|-- histogram: array (nullable = false)
|    |-- element: integer (containsNull = false)

Author:
Siham Amara
Version:
Jan 2022