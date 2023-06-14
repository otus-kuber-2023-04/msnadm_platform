# msnadm_platform
msnadm Platform repository

## kubernetes-intro
### Выполнено
- Развернут minikube ( https://kubernetes.io/docs/tasks/tools/install-minikube/ );
- Добавлен Dashboard (команда `minikube addons enable dashboard`, зайти в панель - команда `minikube dashboard`);
- Проверено, что контейнеры восстанавливаются после удаления;
- Создан Dockerfile, который запускает nginx сервер на 8000 порту под пользователем с uid 1001, который показывает статические файлы из директории /app
- Был создан k8s манифест для образа созданного в предыдущем пункте. initContainers секция содержит скрипт который генерирует index.html в директории /app
- Был создан frontend-pod-healthy.yaml манифест, который запускает frontend образ. В манифесте установлено значение для переменной окружения PRODUCT_CATALOG_SERVICE_ADDR 

### Как запустить проект:
Применить манифест kubectl apply -f web-pod.yml
Как проверить работоспособность:
kubectl port-forward --address 0.0.0.0 pod/web 8000:8000
перейти по ссылке http://localhost:8000/index.html

### Задание со звездочкой:
- Манифесты компонентов `control-plane` хранятся в директории `/etc/kubernetes/manifests` на мастер нодах и служба `kublet` постоянно проверяет их работоспособность. `kube-apiserver` запускается и рестартует через Systemd Service, а `coredns` - контролируется самим k8s через ReplicaSet.
- Причина не запуска является отстутсвие в манифесте заданных параметров сред окружения(ENV).
