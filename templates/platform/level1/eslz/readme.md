
### Management
Deploy Enteprise Scale

```bash
# login a with a user member of the caf-maintainers group
rover login -t {{ config.tenant_name }}.onmicrosoft.com

cd {{ config.destination_install_path }}landingzones
git fetch origin
git checkout {{ config.eslz.private_lib[config.eslz.private_lib.version_to_deploy].caf_landingzone_branch }}

export ARM_USE_AZUREAD=true
caf_env="{{ config.launchpad.caf_environment }}"

rover \
  -lz {{ config.destination_install_path }}landingzones/caf_solution/add-ons/caf_eslz \
  -var-folder {{ config.destination_install_path }}{{ config.destination_relative_base_path }}/{{ level }}/{{ base_folder }} \
  -tfstate {{ tfstates.eslz.tfstate }} \
  -env ${caf_env} \
  -level {{ level }} \
  -a plan

rover logout

```