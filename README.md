# ansible-vertica-exporter
Ansible role for prometheus vertica-exporter

You can use dashboard [`grafana-vertica`](https://github.com/architector-yt-ru/grafana-vertica)

## Description

Vertica-exporter is a fork of `postgres_exporter`](https://github.com/wrouesnel/postgres_exporter) with tiny patch:

```diff
diff --git a/cmd/postgres_exporter/postgres_exporter.go b/cmd/postgres_exporter/postgres_exporter.go
index 1a9eaaa..98bd97a 100644
--- a/cmd/postgres_exporter/postgres_exporter.go
+++ b/cmd/postgres_exporter/postgres_exporter.go
@@ -121,7 +121,7 @@ type UserQuery struct {
 type UserQueries map[string]UserQuery

 // Regex used to get the "short-version" from the postgres version field.
-var versionRegex = regexp.MustCompile(`^\w+ ((\d+)(\.\d+)?(\.\d+)?)`)
+var versionRegex = regexp.MustCompile(`((\d+)(\.\d+)?(\.\d+)?)`)
 var lowestSupportedVersion = semver.MustParse("9.1.0")

 // Parses the version of postgres into the short version string we can use to

```

You can build your own binary and replace `./vertica-exporter/files/vertica_exporter`](https://github.com/architector-yt-ru/ansible-vertica-exporter/blob/master/vertica-exporter/files/vertica_exporter)

## Role variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    vertica_exporter_user: "dbadmin"

Vertica user.

    vertica_exporter_pass: "dbpassword"

User password.

    vertica_exporter_port: 5433

Vertica port.

    vertica_exporter_listen: ':9187'

Address to listen on for web interface and telemetry.

## Example Playbooks

    ---
    - hosts: 
        - vertica
      become: true
      any_errors_fatal: True
      roles:
        - { role: vertica-exporter, tags: [vertica, vertica-exporter] }

      vars:

        vertica_exporter_user: dbadmin
        vertica_exporter_pass: dbpassword
        vertica_exporter_port: 5433
        vertica_exporter_listen: "0.0.0.0:9187"

## Metrics
* vertica_error_messages_count
* vertica_load_balance_policy
* vertica_node_node_state_int
* vertica_projection_storage_ros_count
* vertica_query_active_user_session_count
* vertica_query_executed_query_count
* vertica_query_running_query_count
* vertica_query_total_system_session_count
* vertica_query_total_user_session_count
* vertica_resource_pool_general_memory_borrowed_kb
* vertica_resource_pool_memory_inuse_kb
* vertica_resource_pool_running_query_count
* vertica_resource_queues_memory_requested_kb_total
* vertica_resource_rejections_rejection_count
* vertica_resource_usage_active_thread_count
* vertica_resource_usage_memory_requested_kb
* vertica_resource_usage_request_count
* vertica_resource_usage_ros_row_count
* vertica_resource_usage_ros_used_bytes
* vertica_resource_usage_wos_row_count
* vertica_resource_usage_wos_used_bytes
* vertica_sessions_count
* vertica_storage_containers_delete_vector_count
* vertica_storage_usage_usage_percent
* vertica_system_current_fault_tolerance


## Dependencies

None.

## License

MIT

## Author Information

(c) architector-yt-ru 