# Current Operator version
VERSION ?= 1.6.5

# Name
BUNDLE_NAME ?= istio-operator

# Default bundle image tag
BUNDLE_IMG ?= harbor-b.alauda.cn/aml/$(BUNDLE_NAME)-bundle:$(VERSION)
INDEX_IMG ?= harbor-b.alauda.cn/aml/$(BUNDLE_NAME)-index:$(VERSION)

ORI ?= docker

ALAUDA_INDEX_IMG ?= harbor-b.alauda.cn/3rdparty/operators-index:v3.0.1-82.ge47e2c1

gen-dockerfile:
	opm alpha bundle generate -d bundle/manifests --package $(BUNDLE_NAME) --channels stable,beta --default stable --output-dir fy2

bundle-gen:
	opm alpha bundle build -d bundle/manifests --tag $(BUNDLE_IMG)  --package $(BUNDLE_NAME) --channels alpha --default alpha
bundle-push:
	docker push $(BUNDLE_IMG)

add-index:
	opm index add --bundles $(BUNDLE_IMG) --tag $(INDEX_IMG) -c $(ORI)

push-index:
	docker push $(INDEX_IMG)

append-index:
	opm index add --bundles $(BUNDLE_IMG) --tag $(INDEX_IMG) --from-index $(ALAUDA_INDEX_IMG) -c docker