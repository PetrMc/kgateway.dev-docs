https://github.com/solo-io/gloo/blob/376ba9016cbb6a344667c6403040e4ebf3f92fd2/Makefile#L191C1-L192C35


go run fybrik.io/crdoc@v0.6.4 --resources install/helm/kgateway/crds --output docs/ref.md
go run fybrik.io/crdoc@v0.6.4 --resources ../kgateway/install/helm/kgateway/crds --output ../kgateway.dev-docs/content/docs/reference/api/crdocs-main/_index.md

# for timflannagan/feat/enable-kubectl-explain
go run fybrik.io/crdoc@v0.6.4 --resources ../kgateway/install/helm/kgateway/crds --output ../kgateway.dev-docs/content/docs/reference/api/crdocs-tim/_index.md


# from go types:
mkdir -p ../kgateway.dev-docs/content/docs/reference/api/crd-ref-docs-from-api
mkdir -p ../kgateway.dev-docs/content/docs/reference/api/crd-ref-docs-from-api-group
go run github.com/elastic/crd-ref-docs@v0.1.0 --source-path="../kgateway/api/v1alpha1/" --renderer=markdown --output-path ../kgateway.dev-docs/content/docs/reference/api/crd-ref-docs-from-api/_index.md --config=../kgateway.dev-docs/content/docs/reference/api/data/apidoc.yaml 
go run github.com/elastic/crd-ref-docs@v0.1.0 --source-path="../kgateway/api/v1alpha1/" --renderer=markdown --output-mode=group --output-path ../kgateway.dev-docs/content/docs/reference/api/crd-ref-docs-from-api-group/ --config=../kgateway.dev-docs/content/docs/reference/api/data/apidoc.yaml 

sed Gloo Edge
