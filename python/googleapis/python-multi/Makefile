.PHONY: build
build:
	docker build -t googleapis/python-multi:${TAG} .

.PHONY: publish
publish: build
	docker push googleapis/python-multi:${TAG}
	docker tag googleapis/python-multi gcr.io/cloud-devrel-kokoro-resources/python-multi
	gcloud docker -- push gcr.io/cloud-devrel-kokoro-resources/python-multi
