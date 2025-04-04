# .github
#include <opencv2/cv.h>
#include <opencv2/highgui.h>

int main() {
    CvCapture* capture = cvCaptureFromCAM(0);  // Open default camera
    if (!capture) {
        printf("Cannot access the camera\n");
        return -1;
    }

    cvNamedWindow("Camera", CV_WINDOW_AUTOSIZE);

    while (1) {
        IplImage* frame = cvQueryFrame(capture);
        if (!frame) break;

        cvShowImage("Camera", frame);

        if ((cvWaitKey(10) & 255) == 27) break; // ESC to exit
    }

    cvReleaseCapture(&capture);
    cvDestroyWindow("Camera");

    return 0;
}
