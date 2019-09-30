<!--
 * @Description: Enter here.
 * @Author: Sean@HFHS
 * @Date: 2019-09-27 20:21:23
 * @LastEditors: Sean@HFHS
 * @LastEditTime: 2019-09-30 05:45:03
 -->
### Building Docker image
`docker build --rm --force-rm -t sean/ml-notebook .`

### Running Jupyter server on Docker container
`docker run --rm -p 10000:8888 -v "$PWD":/home/jovyan/work sean/ml-notebook`

### Access Jupyter notebook
http://127.0.0.1:10000

### Permission issue
Once the repo is cloned, make sure to run these 2 commands to fix permission issue as the `Docker` container is running `jovyan` as its user.

`chmod o+w UCI_Diabetes/`
`chmod o+w UCI_Diabetes/UCI_Diabetes.ipynb`