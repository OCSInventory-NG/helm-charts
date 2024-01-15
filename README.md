![Logo-OCS](http://cdn.ocsinventory-ng.org/common/banners/banner300px.png)

# OCS Inventory Helm Chart

## Some Links
  - [ASK question](https://ask.ocsinventory-ng.org)
  - [Website](https://www.ocsinventory-ng.org/?utm_source=github-ocs)
  - [Github](https://github.com/OCSInventory-NG)
  - [OCS Professional](https://ocsinventory-ng.org/?page_id=140&lang=en)

OCS (Open Computers and Software Inventory Next Generation) is an assets management and deployment solution.
Since 2001, OCS Inventory NG has been looking for making software and hardware more powerful.
OCS Inventory NG asks its agents to know the software and hardware composition of every computer or server.

----------

## Assets management

Since 2001, OCS Inventory NG has been looking for making software and hardware more powerful. OCS Inventory NG asks its agents to know the software and hardware composition of every computer or server. OCS Inventory also ask to discover network’s elements which can’t receive an agent. Since the version 2.0, OCS Inventory NG take in charge the SNMP scans functionality.
This functionality’s main goal is to complete the data retrieved from the IP Discover scan. These SNMP scans will allow you to add a lot more informations from your network devices : printers, scanner, routers, computer without agents, …

----------

## Deployment

OCS Inventory NG includes the packet deployment functionality to be sure that all of the softwares environments which are on the network are the same. From the central management server, you can send the packets which will be downloaded with HTTP/HTTPS and launched by the agent on client’s computer. The OCS deployment is configured to make the packets less impactable on the network. OCS is used as a deployment tool on IT stock of more 100 000 devices.

----------

## Used versions

This chart was developped, tested and validated with : 

* v1.24.13 kubernetes API
* v3.13.0 helm version
* v1.28.2 kubectl version

If you have any issues using any other version of Kubernetes / Helm charts, feel free to open an issue.

## Get the Chart

### Add Helm repository

```bash
helm repo add ocsinventory https://ocsinventory-ng.github.io/helm-charts
helm repo update
```

### Retrieve the values.yaml 

```bash
wget https://raw.githubusercontent.com/OCSInventory-NG/helm-charts/main/charts/ocsinventory/values.yaml
```

Note : all parameters on values.yaml are explained in the "Values" section of the README

### Installing the Chart

```bash
cd OCSInventory-Helm-Chart
helm -n <namespace> install <release_name> ocsinventory/ocsinventory -f ./values.yaml --create-namespace
```

### Upgrading the Chart

```bash
helm -n <namespace> upgrade <release_name> ocsinventory/ocsinventory -f ./values.yaml
```

### Uninstalling the Chart

```bash
helm uninstall -n <namespace> <release_name>
kubectl delete ns <namespace>
```

## Usage

To deploy this Helm chart, three operational modes are available:

- Deploy OCS with an existing database: Set externalDatabase.enabled to true;
- Deploy OCS and the database on an existing server: Set database.create to true;
- Deploy OCS, the database server, and the database: Set mariadb.enabled to true.

Based on the chosen option, configure the associated parameters such as
username, password, hostname, database name, and root password. Additional
parameters to configure include persistence.storageClass, ingress.hosts. 

Within the ingress annotations, configure the cluster-issuer and ingress.class. If you
want to authorize only specific IPs or ranges, adjust the whitelist-source-range. 

Lastly, set up the username and password for basic authentication.

## Values

Key | Description | Default
--: | :--: | :--
`image.repository` | ocsinventory Image | `ocsinventory/ocsinventory-docker-image`
`image.pullPolicy` | Image pull policy | `IfNotPresent`
`image.tag` | Image version | `2.12.1`
`replicaCount` | Number of ocs pod to deployed | `1`
`phpconfig.ocsinventory.ini` | Additional php.ini configuration | `config`
`persistense.enabled` | Enable persistence using PVC | `true`
`persistense.size` | PVC Storage Request for OCS volume | `10Gi`
`persistense.accessMode` | PVC Access Mode for OCS volume | `ReadWriteOnce`
`persistense.storageClass` | PVC Storage Class for OCS volume | `""`
`persistense.existingClaim` | An Existing PVC name for OCS volume | `""`
`externalDatabase.enalbed` | Whether to use external database | `false`
`externalDatabase.hostname` | Host of the external database | `""`
`externalDatabase.username` | Username of the external database | `""`
`externalDatabase.password` | Password for the user of the external database | `""`
`externalDatabase.database` | Name of the external databse | `""`
`database.create` | Wether to create a OCS database | `false`
`database.db_name` | Database name to create | `""`
`database.db_user` | Database user to create | `""`
`database.db_pass` | Password for the database | `""`
`database.db_server` | Name of the database service | `""`
`mariadb.enabled` | Whether to create a MariaDB server | `true`
`mariadb.auth.rootPasswd` | MariaDB admin password | `""`
`mariadb.auth.database` | Database name to create | `""`
`mariadb.auth.username` | Database user to create | `""`
`mariadb.auth.password` | Password for the user | `""`
`ingress.enabled` | Enable use of ingress controllers | `true`
`ingress.tls` | Use dedicated certificates | `true`
`ingress.hosts` | OCS hosts to create application URLs | `""`
`ingress.annotations` | An array of ingress annotations | `{}`
`ingress.basicauth.enabled`  | Wether to enable basic auth | `"false"`
`ingress.basicauth.username`  | Username for basic auth | `""`
`ingress.basicauth.password`  | Password for basic auth | `""`
`ingress.basicauth.authRealm` | Basic auth directive | `Authentication Required`
`ingress.basicauth.paths` | Paths with basic auth | `/ocsapi` `/ocsinventory`
`resources` | CPU/Memory resource requests/limits for OCS pod | `{}`

## Acknowledgements

We would like to express our deepest gratitude to the following individuals and organizations who have made this project possible:

- **jackExperts**
- **Indiana University Bloomington**

We are also grateful to everyone who contribute by submitting issues, proposing pull requests, and providing feedback and suggestions.

## Contributing

1. Fork it!
2. Create your feature branch: git checkout -b my-new-feature
3. Add your changes: git add folder/file1.php
4. Commit your changes: git commit -m 'Add some feature'
5. Push to the branch: git push origin my-new-feature
6. Submit a pull request !

## License

OCS Inventory Helm Chart is GPLv3 licensed

