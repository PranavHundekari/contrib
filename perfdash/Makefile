all: push

# See pod.yaml for the version currently running-- bump this ahead before rebuilding!
TAG = 0.14

REPO = k8s.gcr.io

perfdash: perfdash.go parser.go config.go downloader.go google-gcs-downloader.go
	CGO_ENABLED=0 GOOS=linux godep go build -a -installsuffix cgo -ldflags '-w' -o perfdash

container: perfdash
	docker build --pull -t $(REPO)/perfdash:$(TAG) .

push: container
	gcloud docker -s $(REPO) -- push $(REPO)/perfdash:$(TAG)

clean:
	rm -f perfdash
