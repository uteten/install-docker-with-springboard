# 踏み台経由のpythonのインストールメモ

    docker run -v $PWD:/root --name test -it -d python
    docker exec -it test /bin/bash
    
    pip3 install psycopg2 --proxy=172.17.0.1:8080
    pip3 install numpy --proxy=172.17.0.1:8080
    pip3 install matplotlib --proxy=172.17.0.1:8080
    pip3 install scipy
    pip3 install sklearn
    
