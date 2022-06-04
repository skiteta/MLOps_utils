# docker related tips
## Image related
  * pull
    * ```docker pull "DOCKER_IMAGE"```
  * build
    * ```docker build -t "TAG_NAME" .```
  * check
    * ```docker images```
  * delete
    * ```docker rmi "IMAGE_ID"```
## Container related
  * run
    * ```docker run --gpus all -v "MOUNT_DIR_FOR_HOST":"MOUNT_DIR_FOR_DOCKER" -it "IMAGE_ID" --rm -m 32g -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix /bin/bash```
    * ※ If you use display that need put this command "xhost: local" 
  * into
    * ```docker exec -it "CONTAINER_ID" /bin/bash```
  * check
    * ```docker container ls```
    * ```docker ps -a```
  * delete
    * ```docker rm "CONTAINER_ID"```