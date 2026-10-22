# fleet-demo

Demo di Fleet (Rancher continuous delivery) per il laboratorio di kong.

- `podinfo/fleet.yaml`: [podinfo](https://github.com/stefanprodan/podinfo) dal chart Helm ufficiale, 2 repliche,
  ingress su https://podinfo.digitalairlines.com con certificato della CA del laboratorio (ClusterIssuer `lab-ca`).

In Rancher: Continuous Delivery → Git Repos → Create, URL `https://github.com/emilianolangella/fleet-demo.git`,
branch `main`, path `podinfo`, destinazione il cluster `rke`.

Per provare un aggiornamento da Git: cambiare `replicaCount` o `ui.message` in `podinfo/fleet.yaml`, commit e push;
Fleet lo applica da solo entro circa 15 secondi.
