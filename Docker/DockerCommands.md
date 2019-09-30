<!--
 * @Description: Enter here.
 * @Author: Sean@HFHS
 * @Date: 2019-09-27 20:21:23
 * @LastEditors: Sean@HFHS
 * @LastEditTime: 2019-09-30 03:13:34
 -->
### Building Docker image
`docker build --rm --force-rm -t sean/ml-notebook .`

### Running Jupyter server on Docker container
`docker run --rm -p 10000:8888 -v "$PWD":/home/jovyan/work sean/ml-notebook`