# K8s Team operator

This is fork from repo https://github.com/pauljamm/team-operator

Kubernetes Operator allows you to create Team objects with a description of the environment for this Team (for example, developer, QA, Stage environments) and allocates a certain amount of resources for the Team in this Namespace.

## The operator covers the following aspects:
 * Resource Quota in Namespace
 * Limit Range in Namespace
 * RBAC in Namespace

## How the operator works:
- Creates a Namespace called `**TEAM-NAME**`
- Creates LimitRange inside Namespace
- Creates ResourceQouta inside Namespace 
- Creates a serviceaccount for CI
- Creates rolebinding for CI and users

The Operator was tested on K8s version 1.21.2

## Quick start

* Deploing operator with to create the crd value

```
helm install -n kube-system team-operator helm
```


* Describing resources in custom resource definitions for Teams in the yaml manifest and applying it.

Example file for team: `examples/ops_v1_team_cr.yaml`
```
kubectl apply -f examples/ops_v1_team_cr.yaml
```

After applying the yaml manifest with the described resources for Teams the operator creates 3 Namespaces:
 - team-developers
 - team-qa
 - team-stage

```
$ kubectl get namespace

NAME              STATUS   AGE
default           Active   235d
general           Active   235d
kube-node-lease   Active   235d
kube-public       Active   235d
kube-system       Active   235d
logging           Active   211d
monitoring        Active   212d
team-developers   Active   2d15m
team-qa           Active   2d15m
team-stage        Active   2d15m
```

```
$ kubectl describe namespace team-developers

Name:         team-developers
Labels:       inCharge=POK8s
Annotations:  operator-sdk/primary-resource: /team
              operator-sdk/primary-resource-type: Team.ops.southbridge.io
Status:       Active

Resource Quotas
 Name:                   resource-quota
 Resource                Used  Hard
 --------                ---   ---
 limits.cpu              0     2
 limits.memory           0     5Gi
 pods                    0     30
 requests.cpu            0     2
 requests.memory         0     5Gi
 services                0     20
 services.loadbalancers  0     0
 services.nodeports      0     0

Resource Limits
 Type       Resource  Min   Max  Default Request  Default Limit  Max Limit/Request Ratio
 ----       --------  ---   ---  ---------------  -------------  -----------------------
 Container  cpu       50m   1    100m             100m           2
 Container  memory    64Mi  1Gi  100Mi            100Mi          2
```


If you need to increase quotas for Teams, you should change parameters in the `deploy/examples_CR/ops_v1beta1_team_cr.yaml` file and update the custom resource definitions.

## Team
* Pavel Selivanov (pauljamm) : Owner
* Vitaly Fedorov (obsessionsys) : Сontributor

## License
Team-Operator is distributed under MIT. 
See the LICENSE file