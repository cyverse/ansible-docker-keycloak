# Ansible Docker Keycloak
Ansibilized deployment of a Keycloak docker container

# Getting Started
Note: This repo assumes the host you are deploying to already has docker, docker-compose, and ansible installed.

1. Configure your variables inside `hosts.yml.template` and `group_vars/all.template` for your deployment

2. If using/developing custom theme, place or clone it into the corresponding location (see [theme development](#theme-development) for more info)
   ```
   git clone https://github.com/BaoAdrian/keycloak.git /opt/keycloak
   ```

3. Run ansible according to your target
   ```
   sudo ansible-playbook -i <host>.yml playbook.yml

   OR

   sudo ansible-playbook -i <host>.yml playbook.yml --tags="dev"
   ```


## Theme Development
### Usecase
You wish to create or modify a custom theme for Keycloak

### Overview
The development workflow supports creating/editing custom themes for Keycloak by using a mapped volume into the container where themes reside
```
/opt/keycloak/customTheme:/opt/jboss/keycloak/themes/customTheme
```

You may try using this [keycloak custom theme repo](https://github.com/BaoAdrian/keycloak) for starters. This repo is the standard keycloak theme but with the background image of the `login` page removed (just as a basic example)

Simply clone and place it at the aforementioned location on the host and the container will pick up any changes made in this directory and reflect them inside the container.

Once the container is up and running, you should see you `customTheme` inside the Admin Console on the Theme tab. Activate it and return to the login page to see the changes.
