**Ansible Interview Question**
1. How do you manage secrets and sensitive data in Ansible?
I use Ansible Vault to encrypt sensitive data like API keys, passwords, and certificates. I create encrypted files using ansible-vault create or ansible-vault encrypt, and reference them in my playbooks. For CI/CD pipelines, I either store the vault password securely or inject it via environment variables.
________________________________________
2. Difference between roles and tasks?
Tasks are individual units of work in a playbook. Roles are a higher-level abstraction that group tasks, handlers, templates, files, and variables in a standardized structure. I use roles when I need reusability, modularity, and better organization in large-scale playbooks.
________________________________________
3. Difference between when and handlers?
when is used to run tasks conditionally. handlers are triggered only when notified (e.g., when a config file changes).
Example use case: A template task updates an nginx config, and when it does, it notifies a handler to restart nginx—but only if the file actually changed.
________________________________________
4. How do you test playbooks before production?
I use Ansible dry-run mode with --check, and often use Molecule for testing roles. I test in a staging environment that mirrors production, and sometimes use Docker containers for quick testing with Molecule and Testinfra.
________________________________________
5. Have you used dynamic inventory?
Yes. I’ve used AWS dynamic inventory using aws_ec2 plugin to fetch instances based on tags. It’s very useful in cloud environments where servers are dynamic. I configure ansible.cfg to use the dynamic script or plugin.
________________________________________
6. Managing playbooks across environments (dev/test/prod)?
I use group_vars and host_vars directories. Each environment has its own inventory file and set of variables. Sometimes, I use --extra-vars or environment-specific YAML files loaded with vars_files.
________________________________________
7. Handle OS-specific tasks in a single playbook?
I use when: ansible_os_family == 'Debian' or when: ansible_distribution == 'CentOS' to branch logic within the playbook. This way, I can maintain a single playbook that works across different OS families.
________________________________________
8. Integration with CI/CD tools?
Yes. I’ve integrated Ansible with Jenkins and GitLab CI. I write Ansible tasks in pipeline jobs to deploy code, configure servers, and do environment checks. Vault credentials are injected using Jenkins credentials plugin or GitLab secrets.
________________________________________
9. Difference between include and import?
import_tasks is static — it’s processed at playbook parsing time. include_tasks is dynamic — processed during execution.
Use include_tasks when you want to include conditionally (e.g., inside a loop or under a when).
________________________________________
10. How do you optimize playbook execution time?
I use:
•	serial to parallelize tasks in batches.
•	delegate_to for centralized tasks (like notifying load balancers).
•	async and poll for background tasks.
•	fact_caching to avoid collecting facts repeatedly.



