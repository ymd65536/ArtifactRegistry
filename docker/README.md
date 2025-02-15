# Docker コンテナ イメージを Artifact Registry に保存する

## はじめに

このドキュメントでは、Docker コンテナ イメージを Artifact Registry に保存する方法について説明します。

## ハンズオン（コンテナイメージを管理する）

```bash
export LOCATION=asia-northeast1
```

```bash
gcloud auth configure-docker $LOCATION-docker.pkg.dev
```

```bash
docker pull us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0
```

```bash
export PROJECT_ID=`gcloud config list --format 'value(core.project)'` && echo $PROJECT_ID
```

```bash
docker tag us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0 \
$LOCATION-docker.pkg.dev/$PROJECT_ID/quickstart-docker-repo/quickstart-image:tag1
```

```bash
gcloud artifacts repositories create quickstart-docker-repo \
    --repository-format=docker \
    --location=$LOCATION \
    --description="DESCRIPTION"
```

```bash
docker push $LOCATION-docker.pkg.dev/$PROJECT_ID/quickstart-docker-repo/quickstart-image:tag1
```

```bash
docker pull $LOCATION-docker.pkg.dev/$PROJECT_ID/quickstart-docker-repo/quickstart-image:tag1
```

## まとめ

## おまけ

Artifact Registry のリージョン一覧を取得する。

```bash
gcloud artifacts locations list
```
