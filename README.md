## 자주 쓰는 커맨드 목록

### 도커 시작
```sh
sudo systemctl start docker
```

### 도커 빌드
```sh
sudo docker build --tag $LOCAL_IMAGE:$LOCAL_TAG -f $DOCKERFILE_NAME .
```

### 도커 로컬에서 돌려보기
```sh
docker run -it --rm $LOCAL_IMAGE:$LOCAL_TAG /bin/bash
```

### 도커 푸시
```sh
docker login sgs-registry.snucse.org -u coffeetea99 -p $SGS_SECRET
docker tag $LOCAL_IMAGE:$LOCAL_TAG sgs-registry.snucse.org/ws-rzq8iwdacwjd0/$REMOTE_IMAGE:$REMOTE_TAG
docker push sgs-registry.snucse.org/ws-rzq8iwdacwjd0/$REMOTE_IMAGE:$REMOTE_TAG
```

### 쿠버네이트 파드 만들기
```sh
kubectl apply -f pod-sample.yml  
```
또는  
```sh
kubectl run --rm -it --image sgs-registry.snucse.org/ws-rzq8iwdacwjd0/some/$REMOTE_IMAGE:$REMOTE_TAG temp-pod -- /bin/bash
```

### 쿠버네티스 파드 접속
```sh
kubectl exec sample-pod -it -- /bin/bash
```

### 쿠버네티스 이미지 목록
```sh
kubectl get pods --all-namespaces -o jsonpath="{.items[*].spec.containers[*].image}" |\
tr -s '[[:space:]]' '\n' |\
sort |\
uniq -c
```

### SFTP로 폴더 옮기기
```sh
sftp coffeetea99@martini.snucse.org
(enter password)
put -r (폴더 경로)
get -r (폴더 경로)
```

### GPU 있는지 확인
```py
>>> import torch
>>> torch.cuda.is_available()
True
>>> torch.cuda.device_count()
1
>>> torch.cuda.current_device()
0
>>> torch.cuda.device(0)
<torch.cuda.device at 0x7efce0b03be0>
>>> torch.cuda.get_device_name(0)
'GeForce GTX 950M'
```

```py
import torch
print(torch.cuda.is_available())
print(torch.cuda.device_count())
print(torch.cuda.current_device())
print(torch.cuda.device(0))
print(torch.cuda.get_device_name(0))
```
