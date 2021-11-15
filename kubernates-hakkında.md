# kubernates hakkında
kubernates(k8s) konteynerlanmış iş yüklerini(programlar) yönetmeyi sağlayan bir platformdur.

Kubernates; Programları, ağ yapılandırmalarını ve depolamayı hostlar(altyapı sağlayıcıları) arasında sorunsuz bir taşınabilirlik sağlayarak bir nevi orkestra eder.

Kubernates içerisinde belirli bir dallanma hiyerarşisi mevcuttur bu:
` cluster > node > pod > deployment `
olarak belirtilmiştir.

## cluster
Makine kümesidir. nodes olarak adlandırılır. konteynerlanmış uygulamaları yöneten makinelerdir.
## node
işçi makinedir. konteynerlanmış uygulamaları yöneten makinedir.
## pod
En küçün ve en basit kubernate objesidir. Konteynerları barındırır.
### labels
podların özlükleri labelda tutulur. isim gibi.
## container
Uygulumayı ve bağımlılıklarını(dependency) barındıran çalıştırılabilir imaj dosyasıdır.
## deployment
Uygulumanın yapılandırılması için gerekli routinelerin, protokollerin ve araçların replikalarını yönetmeye yarayan bir soyutlamadır. benim xxx-depl olarak isimlendirdiğim yaml dosyaları.
## namespace
Mevcut fiziksel makinede(cluster) birden fazla sanal clusterı destekleyen soyutlamadır.
## service
Podda çalışan uygulamayı ağ alt yapısını kullanarak dışarı açmamızı sağlayan soyutlamadır. benim xxx-srv olarak isimlendirdiğim yaml dosyaları.



## PersistentVolumeClaim
sabit diskte kubernatein ayırdığı belirli alanlardır.
db mizi kurmak için bir volume gerekiyor ve bu alanı pvc ile oluşturucaz

### ``kubectl apply``
`apply` komutu kubernetes resource dosyalarını yönetmemizi sağlar.

cluster içerisindeki resource lerimizi oluşturmak veya güncellemek için bu komutu kullanırız.
örnek kullanımları
```
kubectl apply -f ./my-manifest.yaml            # create/update resource(s)
kubectl apply -f ./my1.yaml -f ./my2.yaml      # create/update from multiple files
kubectl apply -f ./dir                         # create/update resource(s) in all manifest files in dir
kubectl apply -f https://git.io/vPieo          # create/update resource(s) from url
```

### ``kubectl get``
services, pods, deployment, pv(persistent volume), nodes, secrets ve events görüntülemeyi sağlar.
```
kubectl get services        # servisleri listeler
kubectl get pods            # podları listeler
kubectl get deployments     # deploymentları listeler
kubectl get pv              # persistent volume'ları listeler
kubectl get nodes           # nodeları listeler
kubectl get secrets         # secretları listeler
kubectl get events          # event ları listeler
kubectl get jobs            # jobları listeler
```

### ``kubectl rollout``
rollout komutu deploymentların versiyonlama işlemlerini yapmamızı sağlar.
versiyon hakkında bilgi, versiyonu güncelleme, verisyonu geri alma ve deploymentın geçmişini listelemeyi sağlar.
```
kubectl rollout history deployment/frontend-depl                      # frontend-depl deploymentındaki tüm revizyonları commentleriyle listeler
kubectl rollout undo deployment/frontend-depl                         # bir önceki revizyona döndürür
kubectl rollout undo deployment/frontend-depl --to-revision=2         # belirlenen revizyona döndürür
kubectl rollout status -w deployment/frontend-depl                    # frontend-depl deploymentını revizyon süresince an be an değişiklikleri döker
kubectl rollout restart deployment/frontend-depl                      # frontend-depl deploymentını yeniden başlatır
```

### ``kubectl delete ``
services, pods, deployment, pv(persistent volume), nodes, secrets ve events silmeyi sağlar.
```
kubectl delete -f ./pod.json                                              # pod.json içerisinde tipi ve adı belirtilmiş podları silmeyi sağlar
kubectl delete pod,service baz foo                                        # baz ve foo adlı podları ve serviceleri siler
kubectl delete pods,services -l name=myLabel                              # myLabel ismi verilen label'a ait podları ve servisleri siler
kubectl -n my-ns delete pod,svc --all                                      # my-ns namespace'indeki tüm podları ve servisleri siler
```

### ``kubectl get deployments``
default namespacedeki deploymentları getirir
### ``kubectl get pods``
podları listeler
### ``kubectl get services``
servisleri listeler

### ``kubectl apply -f platforms-depl.yaml``
platforms-depl.yaml konfigüre dosyasını kubernate2e

### ``kubectl rollout restart deployment platforms-depl``
platforms-depl deploymentını kaldırıp tekrar yükler

### ``kubectl get namespaces ``
namespace(cluster)leri getirir

## nginx ingress
``kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.0.4/deploy/static/provider/cloud/deploy.yaml``

yaml yapılandırma dosyası ile eklenir
load balancerdır

### ``kubectl create secret generic mssql --from-literal=SA_PASSWORD="pa55w0rd"``

### ``kubectl get pvc``

### ``kubectl get storageclass``


En detaylı komut cheat sheet'i:

via: jimmysong.io
![kubectl detaylı cheatsheet](https://jimmysong.io/kubernetes-handbook/images/kubernetes-kubectl-cheatsheet.png)
