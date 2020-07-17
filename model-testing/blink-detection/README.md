# Test Blink Detection on TX2

This test borrowed code from https://www.pyimagesearch.com/2017/04/24/eye-blink-detection-opencv-python-dlib/

## Steps

1. run the container with ```docker run --net=host -e DISPLAY=$DISPLAY --privileged -v $PWD:/notebooks --rm --env QT_X11_NO_MITSHM=1 -it erikhou/final_project_tx2:2.0 bash```
2. Inside the container run this command ```python3 detect_blinks.py```
