CHART_REPO := oci://registry.hammerhand.corp/charts
CHART_NAME := agentgateway
CHART_REF  := $(CHART_REPO)/$(CHART_NAME)
NAMESPACE  := hammerhand

.PHONY: deploy deploy-prod lint template diff

deploy:
	helm upgrade --install $(CHART_NAME) $(CHART_REF) \
		-n $(NAMESPACE) --wait

deploy-prod:
	helm upgrade --install $(CHART_NAME) $(CHART_REF) \
		-n $(NAMESPACE) \
		-f values-prod.yaml \
		--wait --timeout 120s

lint:
	helm template $(CHART_NAME) $(CHART_REF) \
		-f values-prod.yaml --debug

template:
	helm template $(CHART_NAME) $(CHART_REF) \
		-n $(NAMESPACE)

diff:
	helm diff upgrade $(CHART_NAME) $(CHART_REF) \
		-n $(NAMESPACE) --values values.yaml
