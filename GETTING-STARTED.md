# Guide 🚀

## Steps

### 🔄 Fork the repo

https://github.com/port-labs/microservices-demo/tree/main

### ✨ Create a free account on Port

https://app.getport.io/signup

### ✉️ Verify your email

Log in to your email and verify your account.

### 🔗 Integrate the repo with Port

1. In this example, we'll use GitHub as our integration source.
   ![Integrations](./docs/assets/pick-git.png)
2. Install the Port GitHub app, and give it the necessary permissions for the forked repo.
3. If it doesn't work, you can manually add the integration in Port by clicking on the top right `Builder` button, and then on the left sidebar, click on `Data sources` and then click on `new data source`.

### 🔧 Configure the monorepo integration

1. Go to the [data-sources](https://app.getport.io/settings/data-sources) page of your portal.
2. Under `Exporters`, click on the GitHub you would like to edit.
   ![monorepoDataSourcesExample](./docs/assets/monorepoDataSourcesExample.png)
3. Click on the `three dots` button on the right.
4. Click on `Edit`.
5. Paste the following configuration in the `Mapping` section on the bottom-left:

```yaml
resources:
  - kind: folder
    selector:
      query: "true"
      folders:
        - path: src/* # Relative path to the folders within the repositories.
          repos: # List of repositories to include folders from.
            - microservices-demo
    port:
      entity:
        mappings:
          identifier: ".folder.name"
          title: ".folder.name"
          blueprint: '"service"'
          properties:
            url: .repo.html_url + "/tree/" + .repo.default_branch  + "/" + .folder.path
            readme: file://README.md
```

6. Click on `Save & Resync`.
7. Wait for the sync to complete.

You've successfully synced your monorepo to Port. Congratulations!

View your service catalog [here](https://app.getport.io/services).

You just created a list of services:
![services](./docs/assets/services.png)

For each service, you have a documentation page:
![service-page](./docs/assets/service-page.png)

For each service, you have a scorecard:
![scorecard](./docs/assets/scorecard.png)

To learn more about what a scorecard is, read more [here](https://www.getport.io/guide/scorecards).
