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
classDef block stroke:#3498db,stroke-width:2px;
classDef task stroke:#4b76bb,stroke-width:2px;
classDef includeTasks stroke:#16a085,stroke-width:2px;
classDef importTasks stroke:#34495e,stroke-width:2px;
classDef includeRole stroke:#2980b9,stroke-width:2px;
classDef importRole stroke:#699ba7,stroke-width:2px;
classDef includeVars stroke:#8e44ad,stroke-width:2px;
classDef rescue stroke:#665352,stroke-width:2px;

  vector-->|Role| Start_Vector
  Start_Vector-->|Task| Get_and_Unarchive_vector_distrib0[get and unarchive vector distrib]:::task
  Get_and_Unarchive_vector_distrib0-->|Task| Move_vector_directory1[move vector directory]:::task
  Move_vector_directory1-->|Task| Create_systemd_service_Vector2[create systemd service vector]:::task
  Create_systemd_service_Vector2-->|Task| Enable_and_start_Vector_service3[enable and start vector service]:::task
  Enable_and_start_Vector_service3-->|Task| Get_vector_config4[get vector config]:::task
  Get_vector_config4-->|Task| Flush_handlers5[flush handlers]:::task
  Flush_handlers5-->vector[vector]

  lighthouse-->|Role| Start_Lighthouse
  Start_Lighthouse-->|Task| Update_apt_cache0[update apt cache]:::task
  Update_apt_cache0-->|Task| Install_required_packages_and_dependencies1[install required packages and dependencies]:::task
  Install_required_packages_and_dependencies1-->|Task| Clone_repository_lighthouse2[clone repository lighthouse]:::task
  Clone_repository_lighthouse2-->|Task| Get_lighthouse_config__nginx_conf_3[get lighthouse config  nginx conf ]:::task
  Get_lighthouse_config__nginx_conf_3-->|Task| Get_lighthouse_config__lighthouse_conf_4[get lighthouse config  lighthouse conf ]:::task
  Get_lighthouse_config__lighthouse_conf_4-->|Task| Flush_handlers6[flush handlers]:::task
  Flush_handlers6-->lighthouse[lighthouse]

  Start-->|Include vars| ___lookup__first_found___params____0[include os family specific variables<br>include_vars:    lookup  first found   params    ]:::includeVars
  ___lookup__first_found___params____0-->|Include task| precheck_yml1[unnamed task 1<br>include_task: precheck yml]:::includeTasks
  precheck_yml1-->|Include task| params_yml2[unnamed task 2<br>include_task: params yml]:::includeTasks
  params_yml2-->|Include task| ___lookup__first_found___params____3[unnamed task 3<br>When: **not clickhouse remove bool**<br>include_task:    lookup  first found   params    ]:::includeTasks
  ___lookup__first_found___params____3-->|Include task| configure_sys_yml4[unnamed task 4<br>When: **not clickhouse remove bool**<br>include_task: configure sys yml]:::includeTasks
  configure_sys_yml4-->|Task| Notify_Handlers_Now5[notify handlers now]:::task
  Notify_Handlers_Now5-->|Include task| service_yml6[unnamed task 6<br>include_task: service yml]:::includeTasks
  service_yml6-->|Task| Wait_for_Clickhouse_Server_to_Become_Ready7[wait for clickhouse server to become ready<br>When: **not clickhouse remove bool**]:::task
  Wait_for_Clickhouse_Server_to_Become_Ready7-->|Include task| configure_db_yml8[unnamed task 8<br>When: **not clickhouse remove bool**<br>include_task: configure db yml]:::includeTasks
  configure_db_yml8-->|Include task| configure_dict_yml9[unnamed task 9<br>When: **not clickhouse remove bool**<br>include_task: configure dict yml]:::includeTasks
  configure_dict_yml9-->|Include task| remove_yml10[unnamed task 10<br>When: **clickhouse remove bool**<br>include_task: remove yml]:::includeTasks
  remove_yml10-->End
```

