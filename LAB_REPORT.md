1.Введение

Kubernetes - это система управления контейнерами, которая предназначена для автоматизации развёртывания, масштабирования контейнеризированных приложений.

Kubernetes нужен для:
-автоматизации,
-отказоустойчивости, 
-балансировки нагрузки,
-переносимости, 
-доступности приложений.

2.Шаги выполнения

1) Подготовка окружения:
    kubectl cluster-info
    kubectl get nodes

Проверено подключение к кластеру Kubernetes и наличие активного узла.

2) Работа с Pod'ами:

-Создание Pod:
    kubectl apply -f pod-nginx.yml

-Проверка:
    kubectl get pods

-Просмотр логов:
    kubectl logs nginx-pod

-Удаление Pod:
    kubectl delete pod nginx-pod

3) Создание Deployment:

kubectl apply -f deployment-nginx.yaml
kubectl get pods -o wide
kubectl describe deployment nginx-deployment

Создан Deployment с 3 репликами.

 ![Pods](pods.png)

 4) Создание Service и доступ:
-Создание сервиса:
    kubectl apply -f service-nginx.yaml

-Проверка:
    kubectl get services

-Скриншот списка сервисов:

![Services](services.png)

-Получение URL:
    minikube service nginx-service --url

-Открытие URL в браузере:

![Nginx](nginx.png)

5) Масштабирование:

-Увеличение количества Pod'ов:
    kubectl scale deployment nginx-deployment --replicas=5
    kubectl get pods

-Уменьшение:
    kubectl scale deployment nginx-deployment --replicas=2

6) Обновление приложения:
    kubectl set image deployment/nginx-deployment nginx=nginx:1.21
    kubectl rollout status deployment/nginx-deployment
    kubectl get pods -o jsonpath='{.items[*].spec.containers[*].image}'

7) Откат обновления:
    kubectl rollout undo deployment/nginx-deployment
    kubectl get deployment nginx-deployment -o yaml | grep image

8) Удаление ресурсов:
    kubectl delete -f deployment-nginx.yaml -f service-nginx.yaml

3.Результаты

В результате выполнения лабораторной работы было:

- создано приложение nginx в Kubernetes;
- создан Pod;
- развёрнут Deployment с 3 Pod’ами;
- настроен Service;
- получен доступ к приложению через браузер;
- выполнено масштабирование (увеличение до 5 Pod’ов и уменьшение до 2 Pod’ов);
- выполнено обновление и откат версии nginx;
- удалены все созданные ресурсы.

4.Проблемы и решения

1) Сначала я хотела провести работу через Docker Desktop. Я смогла скачать его, пыталась войти в приложение, оно зависало. Тогда я попробовала сделать так, как рекомендовано на сайте Docker: я создала ключ в терминале в Linux и зашла через него. У меня получилось один раз, но при дальнейшей работе сайт перестал отвечать и приложение не показывало, что я всё-таки смогда войти именно в Desktop версию. 

Я узнала, что, возможно, проблема была в доступе подключения и скорости интернета в момент входа именно в Docker Desktop.

2) Также в процессе выполнения лабораторной работы возникала ошибка отсутствия запущенных Pod’ов, из-за чего сервис был недоступен. 

Решение:

1) Я установила Minikube и выполнила работу через него.

2) Проблема была решена повторным применением Deployment.

5.Выводы:

Благодаря данной лабораторной работе я лучше поняла принципы контейнеризации и оркестрации приложений.

Я изучила основные концепции Kubernetes: Pod, Deployment и Service.

На практике я убедилась, как Kubernetes управляет контейнеризированными приложениями, обеспечивает доступ к ним и позволяет масштабировать их.
