# Kubernetes-Monitoring

Im folgenden werden Prometheus und Grafana deployed.<br>
Der Prometheus Scraper nutzt ausschließlich Daten vom cAdvisor. Dieser ist standardmäßig im Cluster installiert.

## Installation

Diese Repository kann einfach mittels `git clone https://git.sclabs.cloud/soeldner-consult/documentations/kubernetes/kubernetes-monitoring.git` geklont und installiert werden.

---

### [Grafana](../manifests/grafana/)
Das Grafana Deployment besteht aus einem PVC, dem Deployment und einem Service, welcher bei bedarf durch einen Ingress ersetzt werden kann.

`kubectl apply -f manifests/grafana/`

### [Prometheus](../manifests/prometheus)
Damit Prometheus auf den cAdvisor zugreifen kann werden eine Cluster Role und ein Cluster Role Binding benötigt.<br>
Außerdem  gibt es eine ConfigMap für die Scrape Jobs und wieder einen PVC, Service und Deployment.

`kubectl apply -f manifests/prometheus/`

## Konfiguration

Die Standardzugangsdaten für Grafana sind

    username: admin
    password: admin

---

### Datasource Hinzufügen
Die DataSource mit Port 8080 und der **Cluster-IP** anbinden. VMware unterstützt leider keine cluster.local Domains.

`Zahnrad(Links) -> Data Sources -> Add Data Source -> Prometheus`

### Dashboard Importieren
Diese Repository beinhaltet auch ein mit der Scrape Config funktionierendes Dashboard. Dieses kann nun importiert werden.

`Plus(Links) -> Import -> Dashboard JSON einfügen`<br>
[dashboard.json](dashboard.json)
