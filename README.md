# Задание 8-ansible-04-role
Это задание основано на [08-ansible-03-yandex](https://github.com/tvm2360/08-ansible-03-yandex) с применением ролей.

## Роли
| Роли                | Ссылка                                                       |
|---------------------|--------------------------------------------------------------|
| Clickhouse          | https://github.com/AlexeySetevoi/ansible-clickhouse.git      |
| Lighthouse          | https://github.com/tvm2360/08-ansible-04-role-lighthouse     |
| Vector              | https://github.com/tvm2360/08-ansible-04-role-vector         |

| Field                | Value           |
|--------------------- |-----------------|
| Readme update        | 09/02/2025 |

```bash
ansible-galaxy install -r requirements.yml -p roles
```
![GetRoles](./pictures/GetRoles.png)

## requirements.yml
```ansible
- src: git@github.com:AlexeySetevoi/ansible-clickhouse.git
  scm: git
  version: "1.13"
  name: clickhouse
- src: git@github.com:tvm2360/08-ansible-04-role-vector.git
  scm: git
  version: "1.0.0"
  name: vector
- src: git@github.com:tvm2360/08-ansible-04-role-lighthouse.git
  scm: git
  version: "1.0.0"
  name: lighthouse
```

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
classDef block stroke:#3498db,stroke-width:2px;
classDef task stroke:#4b76bb,stroke-width:2px;
classDef includeTasks stroke:#16a085,stroke-width:2px;
classDef importTasks stroke:#34495e,stroke-width:2px;
classDef includeRole stroke:#2980b9,stroke-width:2px;
classDef importRole stroke:#699ba7,stroke-width:2px;
classDef includeVars stroke:#8e44ad,stroke-width:2px;
classDef rescue stroke:#665352,stroke-width:2px;

  Install_Clickhouse -->|Role| Clickhouse
  Clickhouse-->Install_Clickhouse[Install_Clickhouse]

  Install_Lighthouse -->|Role| Lighthouse
  Lighthouse-->Install_Lighthouse[Install_Lighthouse]

  Install_Vector -->|Role| Vector
  Vector-->Install_Vector[Install_Vector]

```

