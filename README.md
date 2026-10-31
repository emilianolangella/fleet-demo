# fleet-demo

Demo di Fleet (Rancher continuous delivery) per il laboratorio di kong.

- `cluster-demo/`: cluster RKE2 `demo-git` in Harvester definito su Git (Rancher provisioning v2 e node driver di
  Harvester): un nodo con tutti i ruoli su 192.168.1.239 e un pool di worker vuoto. GitRepo nel workspace
  `fleet-local` (cluster `local`), path `cluster-demo`. Per la demo: `quantity` del pool `worker` da 0 a 1, commit e
  push; Rancher aggiunge il nodo. Prima della demo `lab/demo/5-cluster-da-git.sh prepara` nel repository kong (secret
  del cloud provider, che non sta qui, e credenziale di Harvester aggiornata in `cluster.yaml`)
- `capi-demo/`: cluster RKE2 `demo-capi` in Harvester definito su Git con oggetti standard di Cluster API
  (`Cluster`, `RKE2ControlPlane`, `MachineDeployment`, `HarvesterCluster` e `HarvesterMachineTemplate`; provider
  CAPRKE2 e CAPHV in Rancher Turtles): un nodo di control plane dietro il LoadBalancer di Harvester su 192.168.1.248 e
  worker da 0 a 1 (`replicas` del MachineDeployment). Nodi Ubuntu 24.04. GitRepo nel workspace `fleet-local`, path
  `capi-demo`. Prima della demo `lab/demo/6-cluster-capi.sh prepara` nel repository kong (provider, immagine, chiave
  SSH, namespace e secret con il kubeconfig di Harvester, che non sta qui)
- `podinfo/fleet.yaml`: [podinfo](https://github.com/stefanprodan/podinfo) dal chart Helm ufficiale, 2 repliche,
  ingress su https://podinfo.digitalairlines.com con certificato della CA del laboratorio (ClusterIssuer `lab-ca`).

In Rancher: Continuous Delivery → Git Repos → Create, URL `https://github.com/emilianolangella/fleet-demo.git`,
branch `main`, path `podinfo`, destinazione il cluster `rke`.

Per provare un aggiornamento da Git: cambiare `replicaCount` o `ui.message` in `podinfo/fleet.yaml`, commit e push;
Fleet lo applica da solo entro circa 15 secondi.
