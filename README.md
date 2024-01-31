<a id="Observability-SRE"></a>
<img src="./assets/images/layout/header.png">

[<img src="./assets/images/icons/java.svg" width="35px" height="35px" alt="Java Logo" title="Java">](https://www.java.com) [<img src="./assets/images/icons/spring.svg" width="25px" height="25px" alt="Spring Logo" title="Spring">](https://spring.io/) [<img src="./assets/images/icons/docker.svg" width="25px" height="25px" alt="Docker Logo" title="Docker">](https://www.docker.com/) [<img src="./assets/images/icons/ubuntu.svg" width="25px" height="25px Logo" title="Ubunto" alt="Ubunto" />](https://ubuntu.com/) [<img src="./assets/images/icons/github.svg" width="25px" height="25px" alt="GitHub Logo" title="GitHub">](https://github.com/jtonynet) [<img src="./assets/images/icons/mysql.svg" width="50px" height="50px" alt="MySQL Logo" title="MySQL">](https://www.mysql.com/) [<img src="./assets/images/icons/redis.svg" width="25px" height="25px" alt="Redis Logo" title="Redis">](https://redis.io/) [<img src="./assets/images/icons/prometheus.svg" width="25px" height="25px" alt="Prometheus Logo" title="Prometheus">](https://prometheus.io/) [<img src="./assets/images/icons/grafana.svg" width="25px" height="25px" alt="Grafana Logo" title="Grafana">](https://grafana.com/) 


<!-- [<img src="./assets/images/icons/jaeger.svg" width="25px" height="25px" alt="Jaeger Logo" title="Jaeger">](https://www.jaegertracing.io/) [<img src="./assets/images/icons/opentelemetry.svg" width="25px" height="25px" alt="OpenTelemetry Logo" title="OpenTelemetry">](https://www.jaegertracing.io/) -->


![Badge Status](https://img.shields.io/badge/STATUS-CLOSED-blue?style=for-the-badge)

---

#### 🕸️ Found me in web:
[![linkedin](https://img.shields.io/badge/Linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/jos%C3%A9-r-99896a39/) [![dev.to](https://img.shields.io/badge/dev.to-0A0A0A?style=for-the-badge&logo=devdotto&logoColor=white)](https://dev.to/learningenuity) [![gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:learningenuity@gmail.com) [![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/aromademirtilo) [![instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/learningenuity) 

---


<a id="index"></a>
## :arrow_heading_up: index

[Observability - SRE](#Observability-SRE)<br/>
  1. :arrow_heading_up: [index](#arrow_heading_up-index)
  2. :green_book: [About](#about)
  3. :computer: [Run the project](#run)
  4. :toolbox: [Tools](#tools)
  5. :clap: [Best Practices](#best-practices)
  6.  :1234: [Versions](#versions)
  7.  :robot: [Use of AI](#ia)

<br/>

[:arrow_heading_up: back to top](#index)

---

<a id="about"></a>
## :green_book: About:


This project aims to study observability and Site Reliability Engineering (SRE) techniques. The purpose is purely didactic, aiming to achieve modern logging and monitoring techniques.

For study and historical reasons, I am keeping the volumes of the Docker images that use this feature, committing them together with the codebase.

The base application made in Java Spring was copied from the course repository and the increments for its observation and monitoring built throughout the [course study track](https://cursos.alura.com.br/formacao-sre)

I must implement the knowledge acquired here in my projects and studies

<br/>

Grafana Images:
<img src="./assets/images/screen_captures/grafana-basic.png">
<img src="./assets/images/screen_captures/grafana-red.png">
<img src="./assets/images/screen_captures/grafana-use.png">

Prometheus - Alerts Green (its OK):
<img src="./assets/images/screen_captures/prometheus-alerts-green.png">

Alertmanger - Alerts Green (its OK):
<img src="./assets/images/screen_captures/alertmanager-alerts-green.png">

 DB and Cache Down (its NOK):
<img src="./assets/images/screen_captures/db-and-cache-down.png">

Prometheus - Alerts Red (its NOK):
<img src="./assets/images/screen_captures/prometheus-alerts-red.png">

Alertmanger - Alerts RED (its NOK):
<img src="./assets/images/screen_captures/alertmanager-alerts-red.png">

Slack Receiving Alerts Red (its NOK):
<img src="./assets/images/screen_captures/slack-alerts.png">

[:arrow_heading_up: back to top](#index)

---

<a id="run"></a>
## :computer: Run the project

With `java 1.8` installed in your machine runs os directory `app`

```bash
mvn clean package
```

And run the 'docker compose up' command (according to your 'docker compose' version) in the project's root directory:
```bash
$ docker compose up
```

Local URLs:
- Grafana - http://localhost:3000/ (user/pwd: admin - admin | admin - 12345)
- Prometheus - http://localhost:9090/
- AlertManager - http://localhost:9093/

<!--
[Import the corresponding JSON](https://grafana.com/docs/grafana/latest/dashboards/manage-dashboards/#import-a-dashboard) into your local Grafana after the proper installation of the project. The JSON file is located in [scripts/grafana-dashboards](./scripts/grafana-dashboards) and add prometheus URL `http://prometheus-forum-api:9090` on datasource connection `http://localhost:3000/connections/datasources/`

<img src="./assets/images/screen_captures/prometheus-datasource-config.png">
-->

<br/>

> :writing_hand: **Note**:
>
> __Troubleshooting with [Docker Volumes](https://betterstack.com/community/questions/what-is-the-best-way-to-manage-permissions-for-docker-shared-volumes/)__
> For the purpose of setting up the local environment, one might encounter issues with permissions in the `docker_data` folders, which stores the volumes of the components needed to run the environment. Does not grant it the necessary permissions to manage these volumes. The approach we are currently using to handle this is to run the following command in case you encounter an error on the first attempt of `docker compose up`:
>```bash
>sudo chmod -R 777 grafana/
>sudo chmod -R 777 prometheus/
>sudo chmod -R 777 alertmanager/
>``` 

<br/>


To use the Slack integration as seen in the "About" section, it will be necessary to configure the [Incoming Webhook](https://api.slack.com/messaging/webhooks) and modify [alertmanager.yml](./alertmanager/alertmanager.yml), changing line 2 to the corresponding URL for message posting.


```yml
1   global:
2    slack_api_url: 'YOUR-URL-SERVICE-HERE like: https://hooks.slack.com/services/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'
```

[:arrow_heading_up: back to top](#index)

---

<a id="tools"></a>
## :toolbox: Tools

- Language:
  - [Java 1.8](https://www.java.com/pt-BR/)

- Framework & Libs:
  - [Spring](https://spring.io/)


- Infra & Technologies
  - [Docker v24.0.6](https://www.docker.com/)
  - [Docker compose v2.21.0](https://www.docker.com/)
  - [MySQL](https://www.mysql.com/)
  - [Redis](https://redis.io/)
  - [Prometheus](https://prometheus.io/)
  - [Grafana](https://grafana.com/)
  - [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/)


- GUIs:
  - [VsCode](https://code.visualstudio.com/)
  - [DBeaver](https://dbeaver.io/)
  - [Another Redis Desktop Manager](https://github.com/qishibo/AnotherRedisDesktopManager)


<br/>

[:arrow_heading_up: back to top](#index)

---

<a id="best-practices"></a>
## :clap: Best Practices

- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
- [keep a changelog](https://keepachangelog.com/en/1.0.0/)
- [Observability](https://en.wikipedia.org/wiki/Observability_(software)) with:
  - [Prometheus](https://prometheus.io/docs/guides/go-application/)
  - [Grafana](https://grafana.com/)
  - [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/)


<br/>

[:arrow_heading_up: back to top](#index)

---

<a id="versions"></a>
## :1234: Versions:

Version tags are being created manually as studies progress with notable improvements in the project. Each feature is developed on a separate branch, and when completed, a tag is generated and merged into the master branch.

For more information, please refer to the [Version History](./CHANGELOG.md)

<br/>

[:arrow_heading_up: back to top](#index)

---

<a id="ia"></a>
### :robot: Use of AI:

The header figures on this page were created with the help of artificial intelligence and a minimum of retouching and construction in Gimp [<img src="./assets/images/icons/gimp.svg" width="30" height="30 " title="Gimp" alt="Gimp Logo" />](https://www.gimp.org/)


__The following prompts were used, in PT-BR, for creation in [Bing IA:](https://www.bing.com/images/create/)__


<details>
  <summary><b>Programer Detective</b></summary>
"Pessoa programador negro de barba e com oculos redondos e o chapeu caracteristico de sherlock holmes, segurando uma xicara de cafe em frente a um computador e ao lado desse computador uma lupa. Estilo cartoon, cores chapadas, fundo branco para facil remocao"<b>(sic)</b>
</details>

The [Black Future](https://www.dafont.com/pt/search.php?q=black+future&text=SRE+Training&psize=l) font was used

<br/>

AI also helped in some research in this study by being used as a support tool; however, __arts and development are, above all, human creative activities. Value people!__

Hire artists for commercial or more elaborate projects and Learn Ingenuity!

[:arrow_heading_up: back to top](#index)

---

<!--
    I NEED TO KILL THIS APACHE 'de merda!"
        https://www.cyberciti.biz/faq/star-stop-restart-apache2-webserver/
-->