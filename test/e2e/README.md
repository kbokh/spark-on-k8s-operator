# E2E Testing

End-to-end (e2e) testing is automated testing for real user scenarios.

## Build and run test

Prerequisites:
- A running k8s cluster and kube config. We will need to pass kube config as arguments.
- Have kubeconfig file ready.
- Have a Kubernetes Operator for Spark image ready.

e2e tests are written as Go test. All go test techniques apply (e.g. picking what to run, timeout length). Let's say I want to run all tests in "test/e2e/":

```bash
$ go test -v ./test/e2e/ --kubeconfig "$HOME/.kube/config" --operator-image=gcr.io/spark-operator/spark-operator:v2.4.0-v1beta1-latest
```

###Available tests

Note that all tests are run on a live Kubernetes cluster. After the tests are done, the Spark Operator deployment and associated resources (e.g. ClusterRole and ClusterRoleBinding) are deleted from the cluster.

* `basic_test.go`

  This test submits `spark-pi.yaml` contained in `\examples`. It then checks that the Spark job successfully completes with the correct result of Pi.