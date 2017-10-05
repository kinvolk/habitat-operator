# API

The following is a description of the Habitat operator API. To see manifest example files, have a look at the [examples directory](https://github.com/kinvolk/habitat-operator/tree/master/examples).

## ServiceGroup

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| metadata |  | [metav1.ObjectMeta](https://kubernetes.io/docs/api-reference/v1.6/#objectmeta-v1-meta) | true |
| spec |  | [ServiceGroupSpec](#servicegroupspec) | true |
| status |  |  | false |

## ServiceGroupSpec

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| count | Count is the amount of Services that should start in this Service Group. | int | true |
| image | Image is the Docker image of the Habitat Service. | string | true |
| habitat |  | [Habitat](#habitat) | true |

## Habitat

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| group | Group is a logical grouping of services with the same package and topology type connected together in a ring. Defaults to `default`. | string | false |
| topology | A topology describes the intended relationship between peers within a service group. Specify either `standalone` or `leader` topology.  | Topology | true |
| configSecretName | Config is the name of the Kubernetes Secret containing the Config that the user has previously created. Habitat will use it for initial configuration of the service. | string | false |
| ringSecretName | The name of the Kubernetes Secret that contains the ring key, which encrypts the communication between Habitat supervisors. | string | false |
| bind | When one service connects to another forming a producer/consumer relationship. Able to specify multiple binds. | [][Bind](#bind) | false |

## Bind

| Field | Description | Scheme | Required |
| ----- | ----------- | ------ | -------- |
| name | Name of the bind specified in the Habitat configuration files. | string | true |
| service | Name of the service this bind refers to. | string | true |
| group | Group of the service this bind refers to. | string | true |