# devops
This is my BRAC M&amp;E Team (One of the team of BRAC M&amp;E) DevOps Related work repository

## Create New Branch
```bash
BRANCH=rc
NEW_BRANCH=legacy_rc
CLIENT_PATH=/home/ubuntu/pipelines/workspace/Brac/mne_release_uat/brac_docker_compose/client
BACKEND_PATH=/home/ubuntu/pipelines/workspace/Brac/mne_release_uat/brac_docker_compose/backend
create_branch_on_modules () {
git fetch
git checkout ${BRANCH}
git merge origin ${BRANCH}
git checkout -b ${NEW_BRANCH}
git push origin ${NEW_BRANCH}
git branch
}

recursively_create_branch_on_submodules() {
git submodule foreach git fetch
git submodule foreach git checkout ${BRANCH}
git submodule foreach git merge origin ${BRANCH}
git submodule foreach git checkout -b ${NEW_BRANCH}
git submodule foreach git push origin ${NEW_BRANCH}
git submodule foreach git branch
}
 
checkout_all_backend_modules() {
cd "${BACKEND_PATH}/datasyncmodule"
create_branch_on_modules 
recursively_create_branch_on_submodules

cd "${BACKEND_PATH}/datasyncmodule/mne.core"
create_branch_on_modules 
recursively_create_branch_on_submodules

cd "${BACKEND_PATH}/superset-service"
create_branch_on_modules
}

checkout_all_frontend_modules () {
cd "${CLIENT_PATH}/admin-client"
create_branch_on_modules

cd "${CLIENT_PATH}/auth-client"
create_branch_on_modules

cd "${CLIENT_PATH}/group-management-client"
create_branch_on_modules
    
cd "${CLIENT_PATH}/survey-client"
create_branch_on_modules

cd "${CLIENT_PATH}/event-management-client"
create_branch_on_modules
}

echo "Create hotfix branch Started"
checkout_all_backend_modules
checkout_all_frontend_modules
echo "Create hotfix branch Completed Successfully"
```
# Delete New Branch

```bash
NEW_BRANCH=legacy_rc
CLIENT_PATH=/home/ubuntu/pipelines/workspace/Brac/mne_release_uat/brac_docker_compose/client
BACKEND_PATH=/home/ubuntu/pipelines/workspace/Brac/mne_release_uat/brac_docker_compose/backend
create_branch_on_modules () {
git push origin --delete ${NEW_BRANCH}
git branch
}

recursively_create_branch_on_submodules() {
git submodule foreach push origin --delete ${NEW_BRANCH}
git submodule foreach git branch
}
 
checkout_all_backend_modules() {
cd "${BACKEND_PATH}/datasyncmodule"
create_branch_on_modules 
recursively_create_branch_on_submodules

cd "${BACKEND_PATH}/datasyncmodule/mne.core"
create_branch_on_modules 
recursively_create_branch_on_submodules

cd "${BACKEND_PATH}/superset-service"
create_branch_on_modules
}

checkout_all_frontend_modules () {
cd "${CLIENT_PATH}/admin-client"
create_branch_on_modules

cd "${CLIENT_PATH}/auth-client"
create_branch_on_modules

cd "${CLIENT_PATH}/group-management-client"
create_branch_on_modules

cd "${CLIENT_PATH}/survey-client"
create_branch_on_modules

cd "${CLIENT_PATH}/event-management-client"
create_branch_on_modules
}

echo "Delete hotfix branch Started"
checkout_all_backend_modules
checkout_all_frontend_modules
echo "Delete hotfix branch Completed Successfully"
``

