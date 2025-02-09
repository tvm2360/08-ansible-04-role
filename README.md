# Задание 8-ansible-04-role

## Роли

| Field                | Value           |
|--------------------- |-----------------|
| Readme update        | 09/02/2025 |

## Сценарии

```yml
---
- name: Install Clickhouse
  hosts: clickhouse
  roles:
    - clickhouse
- name: Install Vector
  hosts: vector
  roles:
    - vector
- name: Install Lighthouse
  hosts: lighthouse
  roles:
    - lighthouse

```

```mermaid
flowchart TD
Start
classDef block stroke:#3498db,stroke-width:2px;
classDef task stroke:#4b76bb,stroke-width:2px;
classDef includeTasks stroke:#16a085,stroke-width:2px;
classDef importTasks stroke:#34495e,stroke-width:2px;
classDef includeRole stroke:#2980b9,stroke-width:2px;
classDef importRole stroke:#699ba7,stroke-width:2px;
classDef includeVars stroke:#8e44ad,stroke-width:2px;
classDef rescue stroke:#665352,stroke-width:2px;

  clickhouse-->|Role| clickhouse[clickhouse]
  vector-->|Role| vector[vector]

  lighthouse-->|Role| lighthouse[lighthouse]
  Start-->|Task| Update_apt_cache0[update apt cache]:::task
  Update_apt_cache0-->|Task| Install_required_packages_and_dependencies1[install required packages and dependencies]:::task
  Install_required_packages_and_dependencies1-->|Task| Clone_repository_lighthouse2[clone repository lighthouse]:::task
  Clone_repository_lighthouse2-->|Task| Get_lighthouse_config__nginx_conf_3[get lighthouse config  nginx conf ]:::task
  Get_lighthouse_config__nginx_conf_3-->|Task| Get_lighthouse_config__lighthouse_conf_4[get lighthouse config  lighthouse conf ]:::task
  Get_lighthouse_config__lighthouse_conf_4-->|Task| Flush_handlers5[flush handlers]:::task
  Flush_handlers5-->End
```

