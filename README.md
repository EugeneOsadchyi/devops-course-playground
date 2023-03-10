# DevOps Course

## Table of content
- [DevOps Course](#devops-course)
  - [Table of content](#table-of-content)
  - [Task](#task)
  - [How to work with the repository](#how-to-work-with-the-repository)

## Task

Розгорнути програму в кластері k8s, кластер в свою чергу розгорнути в хмарі. Налаштувати CI/CD на базі Jenkins, підготувати інфраструктуру за допомогою terraform.


1) В якості програми беремо відомий нам проект на базі node.js https://github.com/benc-uk/nodejs-demoapp. На його основі збираємо Docker образ у якому має бути `nginx + node.js app`. Nginx повинен проксирувати запити, що прийшли на 80 порт на 3000 порт програми. Усі необхідні файли для збирання кладіть на github (посилання на нього додаєте до ДЗ).

2) За допомогою Jenkins організуєте забір образу з github, білд образу та розміщення образу в Docker registry (можна на Docker Hub).
    Окремо Jenkins повинен зробити деплой програми у підготовлений, у хмарі k8s кластер.
    Кількість подів у деплої має бути 4.
    Самих деплоїв має бути також 4.
    До кожного деплою необхідно створити сервіс.
    І на завершення встановити та налаштувати ingress. Правила для ingress повинні містити 4 різні імені, кожне з яких призводить до свого сервісу.

    Всі установки та налаштування по максимуму необхідно автоматизувати за допомогою yaml файлів і Jenkins.
    Завдання для Jenkins потрібно зробити через jenkinsfile (його прикладаєте до ДЗ)

3) Майданчик для програми у хмарі має виглядати так:

    Мережа:
    - Створюєте окрему віртуальну мережу із двома підмережами, одна приватна одна публічна. Для приватної мережі організовує вихід в інтернет.
    - Налаштовуєте необхідні правила для трафіку та машрутизацію (якщо потрібно)
    - Можливо, потрібно використовувати балансувальник, а кластер k8s помістити в приватну мережу J

    Розгортаєте кластер k8s (дві ноди буде достатньо).

    У приватній мережі розгортаєте SQL інстанс, приєднуєте його до кластера k8s (для майбутнього використання).

Все, що потрібно для створення майданчика в хмарі, робите за допомогою тераформ, файлики прикладаєте до ДЗ.

## How to work with the repository
1. For applying Terraform infrastructure to your AWS account - [Check steps](./terraform/README.md)
2. For applying K8S infrastructure to AWS EKS or Docker for Desktop - [Check steps](./k8s/README.md)
3. You need a `Jenkins` instance, which does Docker image build + upload and applying it to the kubernetes cluster.
   Make sure, it has an access to Docker and Kubernetes CLI.
