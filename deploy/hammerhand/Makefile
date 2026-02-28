CHART_REPO := oci://registry.hammerhand.corp/charts
CHART_NAME := agentgateway
NAMESPACE  := hammerhand

.PHONY: deploy deploy-prod lint template

deploy:
	helm upgrade --install $(CHART_NAME) $(CHART_REPO)/$(CHART_NAME) \
		-n $(NAMESPACE) --wait

deploy-prod:
	helm upgrade --install $(CHART_NAME) $(CHART_REPO)/$(CHART_NAME) \
		-n $(NAMESPACE) \
		-f values-prod.yaml \
		--wait --timeout 120s

lint:
	helm template $(CHART_NAME) $(CHART_REPO)/$(CHART_NAME) \
		-f values-prod.yaml --debug

template:
	helm template $(CHART_NAME) $(CHART_REPO)/$(CHART_NAME) \
		-n $(NAMESPACE)
