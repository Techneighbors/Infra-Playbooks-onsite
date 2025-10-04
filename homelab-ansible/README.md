# Home Lab Ansible Automation

This repository contains a collection of simple Ansible playbooks designed to automate the setup and management of a home lab environment.

## Project Structure

- **playbooks/**: Contains the main playbooks for various tasks.
  - `setup-webserver.yml`: Playbook for setting up a web server.
  - `update-systems.yml`: Playbook for updating system packages.

- **inventory/**: Defines the hosts and variables for Ansible.
  - `hosts.yml`: Inventory file listing the target machines.
  - `group_vars/`: Contains variables that apply to all hosts.
    - `all.yml`: Centralized variables for all hosts.

- **roles/**: Contains reusable roles for organizing tasks and configurations.
  - `common/`: A role with common tasks and configurations.
    - `tasks/main.yml`: Main tasks for the common role.
    - `handlers/main.yml`: Handlers for the common role.
    - `vars/main.yml`: Variables specific to the common role.

- **ansible.cfg**: Configuration file for Ansible, specifying settings and paths.

## Usage

1. Clone the repository to your local machine.
2. Update the `inventory/hosts.yml` file with your target machines.
3. Modify any necessary variables in `inventory/group_vars/all.yml`.
4. Run the desired playbook using the following command:

   ```
   ansible-playbook playbooks/<playbook_name>.yml
   ```

Replace `<playbook_name>` with either `setup-webserver` or `update-systems`.

## Contributing

Feel free to contribute by adding new playbooks, roles, or improving existing ones. Please ensure that your contributions adhere to the project's structure and guidelines.

## License

This project is licensed under the MIT License. See the LICENSE file for details.