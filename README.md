# Ansible Docker Keycloak

Ansibilized deployment of a Keycloak docker container

# Getting Started

Note: This repo assumes the host you are deploying to already has docker, docker-compose, and ansible installed.

1. Configure your inventory inside a file named `hosts.yml`. You may use `hosts.yml.template` as a starting point.

2. Configure your group variables inside a file named `group_vars/all`. You may use `group_vars/all.template` as a
   starting point.

3. If using/developing custom theme, place or clone it into a subdirectory named `themes` within the keycloak
   distribution directory (value of the `KEYCLOAK_DIST_DIR` group variable or `/opt/keycloak` by default) on the hosts
   where Keycloak will be running. For example, if you're cloning a repository and using the default distribution
   directory, you could enter the following commands:

   ```
   mkdir -p /opt/keycloak/themes
   git clone https://github.com/example-org/theme-repo.git /opt/keycloak/themes/theme1
   ```

4. If using/developing custom themes, add the theme names to the `KEYCLOAK_CUSTOM_THEMES` group variable. For example:

   ```
   KEYCLOAK_CUSTOM_THEMES = [theme1]
   ```

5. Run ansible according to your target

   ```
   sudo ansible-playbook -i <host>.yml playbook.yml

   OR

   sudo ansible-playbook -i <host>.yml playbook.yml --tags="dev"
   ```


## Theme Development

### Usecase

You wish to create or modify a custom theme for Keycloak

### Overview

The development workflow supports creating/editing custom themes for Keycloak by using a mapped volume into the
container where themes reside in

```
/opt/keycloak/themes/theme-name:/opt/jboss/keycloak/themes/theme-name
```

where `/opt/keycloak` is the customizable Keycloak distribution directory (see the instructions above) and `theme-name`
is the name of the theme that you're developing.

You may try using this [keycloak custom theme repo](https://github.com/BaoAdrian/keycloak) for starters. This repo is
the standard keycloak theme but with the background image of the `login` page removed (just as a basic example).

Simply clone and place it at the aforementioned location on the host and the container will pick up any changes made in
this directory and reflect them inside the container.

Once the container is up and running, you should see `customTheme` inside the Admin Console on the Theme tab. Activate
it and return to the login page to see the changes.
