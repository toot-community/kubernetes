$ kubectl create namespace istio-system
$ helm install istio-base istio/base -n istio-system
$ helm install istiod istio/istiod -n istio-system --values ~/Development/toot.community/kubernetes/istio/istio-istiod.values.test.yaml --wait

$ kubectl create namespace istio-ingress
$ kubectl label namespace istio-ingress istio-injection=enabled
$ helm install istio-ingress istio/gateway --values ~/Development/toot.community/kubernetes/istio/istio-gateway.values.test.yaml -n istio-ingress --wait

$ kubectl label namespace tootcommunity istio-injection=enabled
$ kubectl label namespace haproxy istio-injection=enabled

$ helm install \
--namespace istio-system \
--set auth.strategy="anonymous" \
--repo https://kiali.org/helm-charts \
kiali-server \
kiali-server
