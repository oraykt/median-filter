
Here is it basic Cpp smoothin codes
function {

#include<iostream>
#include<opencv2/imgproc/imgproc.hpp>
#include<opencv2/highgui/highgui.hpp>

using namespace std;
using namespace cv;

int insertionSort(int med[])
{
	int temp, i, j;
	for (i = 0; i < 9; i++) {
		temp = med[i];
		for (j = i - 1; j >= 0 && temp < med[j]; j--) {
			med[j + 1] = med[j];
		}
		med[j + 1] = temp;
	}
	return med[4];
}
int main() {
	Mat source, mean9, mean16, median;
	source = imread("C:\\Users\\Oray\\Documents\\Visual Studio 2015\\Projects\\Project1\\Resimler\\median.png", CV_LOAD_IMAGE_GRAYSCALE);
	if (!source.data) {
		cout << "Resim yüklenmedi" << endl;	 // Img not loaded
		return -1;
	}
	median = source.clone();
	for (int x = 1; x < source.rows - 1; x++) {
		for (int y = 1; y < source.cols - 1; y++) {
			int kernelMedian[9], k=0;
			for (int i = -1; i <= 1; i++) {
				for (int j = -1; j <= 1; j++) {
					kernelMedian[k] = source.at<uchar>(x + i, y + j);
					k++;
				}
			}
			median.at<uchar>(x, y) = insertionSort(kernelMedian);
		}
	}
	imshow("Orginal", source);
	imshow("Median", median);
	waitKey(0);
	return 0;
}
}
