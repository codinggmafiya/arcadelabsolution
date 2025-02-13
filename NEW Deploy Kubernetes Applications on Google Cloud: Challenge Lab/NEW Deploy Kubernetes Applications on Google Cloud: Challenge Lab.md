# APIs Explorer: Cloud Storage || [GSP318](https://www.cloudskillsboost.google/games/5890/labs/37471) ||

### Run the following Commands in CloudShell

START FROM HERE . PUT THE VALUES FROM LAB .

```
export IMAGE=
export TAG=
export REPOSITORY=
export PROJECTID=
```

TASK - 1  

RUN IN CLOUD SHELL

```
source <(gsutil cat gs://cloud-training/gsp318/marking/setup_marking_v2.sh)
```

```
gsutil cp gs://spls/gsp318/valkyrie-app.tgz .
tar -xzf valkyrie-app.tgz
cd valkyrie-app
```

```
gsutil cat gs://cloud-training/gsp318/marking/setup_marking.sh | bash
 
 
gsutil cp gs://spls/gsp318/valkyrie-app.tgz .
tar -xzf valkyrie-app.tgzcd valkyrie-app
 
cat > Dockerfile <<EOF
FROM golang:1.10
WORKDIR /go/src/app
COPY source .
RUN go install -v
ENTRYPOINT ["app","-single=true","-port=8080"]
EOF
 
docker build -t $IMAGE:$TAG .  
cd ..
 
cd marking
 
./step1_v2.sh
```

TASK - 2

```
cd ..
 
cd valkyrie-app
 
docker run -p 8080:8080 $IMAGE:$TAG &
```

PRESS cntrl + c

```
cd ..
 
cd marking
 
./step2_v2.sh

bash ~/marking/step2_v2.sh
```

TASK - 3 ( REPLACE YOUR REGION  AND ZONE)

```
cd ..
 
cd valkyrie-app
 
gcloud artifacts repositories create $REPOSITORY --repository-format=Docker \
--location=<REPLACE YOUR REGION>
 
docker tag $IMAGE:$TAG <REPLACE YOUR REGION>-docker.pkg.dev/$PROJECTID/$REPOSITORY/$IMAGE:$TAG
 
docker-credential-gcr configure-docker --registries=<REPLACE YOUR ZONE>-docker.pkg.dev
 
docker push <REPLACE YOUR REGION>-docker.pkg.dev/$PROJECTID/$REPOSITORY/$IMAGE:$TAG
```

TASK - 4  (  REPLACE ALONG WITH <REPLACE> WIH YOUR ACTUAL REGION OR ZONE )
RUN IN CLOUD SHELL 
```
source <(gsutil cat gs://cloud-training/gsp318/marking/setup_marking_v2.sh)
```

```
gsutil cp gs://spls/gsp318/valkyrie-app.tgz .
tar -xzf valkyrie-app.tgz
cd valkyrie-app
```


```
sed -i  s#IMAGE_HERE#<REPLACE YOUR REGION>-docker.pkg.dev/$PROJECTID/$REPOSITORY/$IMAGE:$TAG#g k8s/deployment.yaml
 
gcloud container clusters get-credentials valkyrie-dev --zone <REPLACE YOUR ZONE>
 
kubectl create -f k8s/deployment.yaml
 
kubectl create -f k8s/service.yaml

gcloud auth configure-docker <REPLACE YOUR ZONE>-docker.pkg.dev
```

WAIT 2 MINUTES THE CHECK MY PROGRESS

### Congratulations 🎉 for Completing the Lab !

# [CODINGG MAFIYA](https://www.youtube.com/@CodinggMafiya)


