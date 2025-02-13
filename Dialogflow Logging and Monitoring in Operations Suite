# APIs Explorer: Cloud Storage || [GSP794](https://www.cloudskillsboost.google/games/5890/labs/37470) ||

### Run the following Commands in CloudShell

START FROM HERE . PUT THE VALUES FROM LAB .

```
export IMAGE=
export TAG=
export REPOSITORY=
export PROJECTID=
```

TASK - 1  

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
```

TASK - 3  (<REPLACE YOUR REGION> AND ZONE)

```
cd ..
 
cd valkyrie-app
 
gcloud artifacts repositories create $REPOSITORY --repository-format=Docker \
--location=<REPLACE YOUR REGION>
 
docker tag $IMAGE:$TAG <REPLACE YOUR REGION>-docker.pkg.dev/$PROJECTID/$REPOSITORY/$IMAGE:$TAG
 
docker-credential-gcr configure-docker --registries=<REPLACE YOUR ZONE>-docker.pkg.dev
 
docker push <REPLACE YOUR REGION>-docker.pkg.dev/$PROJECTID/$REPOSITORY/$IMAGE:$TAG
```

TASK - 4  ( <REPLACE YOUR ZONE> REPLACE ALONG WITH <> WIH YOUR ACTUAL REGION OR ZONE )

```
sed -i  s#IMAGE_HERE#<REPLACE YOUR REGION>-docker.pkg.dev/$PROJECTID/$REPOSITORY/$IMAGE:$TAG#g k8s/deployment.yaml
 
gcloud container clusters get-credentials valkyrie-dev --zone <REPLACE YOUR ZONE>
 
kubectl create -f k8s/deployment.yaml
 
kubectl create -f k8s/service.yaml

gcloud auth configure-docker <REPLACE YOUR ZONE>-docker.pkg.dev
```

### Congratulations 🎉 for Completing the Lab !

# [CODINGG MAFIYA](https://www.youtube.com/@CodinggMafiya)

