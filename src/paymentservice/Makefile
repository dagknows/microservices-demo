VERSION=0.0.9
REPO_URL=us-central1-docker.pkg.dev/dagknows-demo-setup/hipster-images
MAKEFILE_DIR:=$(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))
# SVC_ROOT=$(shell dirname $(MAKEFILE_DIR))
SVC_NAME=$(shell basename $(MAKEFILE_DIR))
IMAGE_PATH=$(REPO_URL)/$(SVC_NAME):$(VERSION)
PKGGREP=$(shell gcloud artifacts docker images list $(REPO_URL)/$(SVC_NAME) --include-tags --filter tags=$(VERSION) --format yaml | grep "package:")

printenv:
	@echo REPO_URL=$(REPO_URL)
	@echo MAKEFILE_DIR=$(MAKEFILE_DIR)
	@echo VERSION=$(VERSION)
	@echo IMAGE_PATH=$(IMAGE_PATH)
	@echo PKGGREP=$(PKGGREP)

build:
	@if [ "$(PKGGREP)" != "" ]; then \
  	echo "Image with tag $(VERSION) - $(IMAGE_PATH) already exists.  Increment the version number"; \
  else \
		docker image build . -t $(IMAGE_PATH) ; \
		docker image build . -t $(REPO_URL)/$(SVC_NAME):latest ; \
  fi

push:
	docker push $(IMAGE_PATH)
	docker push $(REPO_URL)/$(SVC_NAME):latest
