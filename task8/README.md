# Task 8 SAP Developer Challenge - APIs - Task 8 - Create an instance of the SAP Cloud Management Service

https://groups.community.sap.com/t5/application-development/sap-developer-challenge-apis-task-8-create-an-instance-of-the/m-p/280681

There are two parts to your task here. In both parts, you should use the cf command line tool for Cloud Foundry (also known as the "cf CLI").
There are different ways you could go about creating a service instance on Cloud Foundry, but here the cf CLI is prescribed because it can be used for not only creating the instance, but also for retrieving detailed information afterwards. And of course, also because #TheFutureIsTerminal 🙂
For part one, you must complete step 1 in the list above, i.e. create an instance of the SAP Cloud Management Service (short name: cis). Do this in your SAP BTP account that you used in the previous task. Make sure you choose the appropriate plan when doing this, and create the instance in your Cloud Foundry environment.

For part two, you must use the Cloud Foundry API to retrieve information about your newly created service instance. Specifically, you should use the List all Service Instances endpoint (GET /v2/service_instances). And as you'll have already been using the cf CLI for part one of this task, you are strongly encouraged to use it for this part as well. Did you know that you can use the cf CLI to make calls to the CF API as well? Find out more in the "Hints and tips section below".
From the information you retrieve via the GET /v2/service_instances endpoint, you should identify the appropriate object in the resources property in the JSON returned, and pick out the value of the entity type.

Try to create the service without using the cockpit.....

<pre>
➜  task8 git:(main) ✗ cf create-service cis central cis
Creating service instance cis in org John Astill_development-hkas66x8 / space dev as john_sap@astill.org...
Invalid service plan. Ensure that the service plan exists, is available, and you have access to it.
FAILED
➜  task8 git:(main) ✗ 
</pre>

So it appears that the Entitlement is not avaiable.

<pre>
➜  task8 git:(main) ✗ btp list accounts/entitlement | grep cis        
cis                                           local                        cis-local                                                                                            ELASTIC_SERVICE                   eu10(cloudfoundry); ap20(cloudfoundry); br10(cloudfoundry); eu20(cloudfoundry); ap11(cloudfoundry); eu30(cloudfoundry); ap21(cloudfoundry); ap10(cloudfoundry); us20(cloudfoundry); us10(cloudfoundry); us21(cloudfoundry); us30(cloudfoundry); ch20(cloudfoundry); ca10(cloudfoundry); in30(cloudfoundry); jp10(cloudfoundry); jp20(cloudfoundry); ap12(cloudfoundry); eu11(cloudfoundry)   Vendor        
cis                                           central                      cis-central                                                                                          ELASTIC_SERVICE                   eu10(cloudfoundry); ap20(cloudfoundry); br10(cloudfoundry); eu20(cloudfoundry); ap11(cloudfoundry); eu30(cloudfoundry); ap21(cloudfoundry); ap10(cloudfoundry); us20(cloudfoundry); us10(cloudfoundry); us21(cloudfoundry); us30(cloudfoundry); ch20(cloudfoundry); ca10(cloudfoundry); in30(cloudfoundry); jp10(cloudfoundry); jp20(cloudfoundry); ap12(cloudfoundry); eu11(cloudfoundry)   Vendor        

OK

➜  task8 git:(main) ✗ 
</pre>


<pre>
➜  task8 git:(main) ✗ btp list accounts/subaccount

subaccounts in global account ba4e2696-0864-46db-b37e-043ef0917ddd...

subaccount id:                         display name:   subdomain:             region:   beta-enabled:   parent id:                             parent type:     state:   state message:        
c811232a-4e80-4847-9888-a938ab3bac95   Development     development-hkas66x8   us10      false           ba4e2696-0864-46db-b37e-043ef0917ddd   global account   OK       Subaccount created.   


OK

➜  task8 git:(main) ✗ 
</pre>


<pre>
➜  task8 git:(main) ✗ btp help assign accounts/entitlement
Usage: btp [OPTIONS] assign accounts/entitlement --global-account [SUBDOMAIN] [--to-subaccount ID] [--to-directory ID] --for-service NAME --plan NAME [--plan-unique-identifier NAME] [--enable] [--amount NUMBER] [--auto-distribute-amount NUMBER] [--auto-assign] [--distribute]

Assign an entitlement to a subaccount or directory.
</pre>

So.....

btp assign accounts/entitlement --global-account --to-subaccount c811232a-4e80-4847-9888-a938ab3bac95 --for-service cis --plan central

<pre>
 task8 git:(main) ✗ btp assign accounts/entitlement --global-account --to-subaccount c811232a-4e80-4847-9888-a938ab3bac95 --for-service cis --plan central 

Assigning global account entitlement to subaccount...

global account id:        ba4e2696-0864-46db-b37e-043ef0917ddd
subaccount id:            c811232a-4e80-4847-9888-a938ab3bac95
service/app name:         cis
service plan name:        central
plan unique identifier:   
enable:                   false

Command runs in the background. 
Use 'btp list accounts/entitlement' to verify status.


OK

➜  task8 git:(main) ✗ 
</pre>


<pre>
➜  task8 git:(main) ✗ btp list accounts/entitlement | grep cis                                                                             
cis                                           local                        cis-local                                                                                            ELASTIC_SERVICE                   eu10(cloudfoundry); ap20(cloudfoundry); br10(cloudfoundry); eu20(cloudfoundry); ap11(cloudfoundry); eu30(cloudfoundry); ap21(cloudfoundry); ap10(cloudfoundry); us20(cloudfoundry); us10(cloudfoundry); us21(cloudfoundry); us30(cloudfoundry); ch20(cloudfoundry); ca10(cloudfoundry); in30(cloudfoundry); jp10(cloudfoundry); jp20(cloudfoundry); ap12(cloudfoundry); eu11(cloudfoundry)   Vendor        
cis                                           central                      cis-central                                                                                          ELASTIC_SERVICE                   eu10(cloudfoundry); ap20(cloudfoundry); br10(cloudfoundry); eu20(cloudfoundry); ap11(cloudfoundry); eu30(cloudfoundry); ap21(cloudfoundry); ap10(cloudfoundry); us20(cloudfoundry); us10(cloudfoundry); us21(cloudfoundry); us30(cloudfoundry); ch20(cloudfoundry); ca10(cloudfoundry); in30(cloudfoundry); jp10(cloudfoundry); jp20(cloudfoundry); ap12(cloudfoundry); eu11(cloudfoundry)   Vendor        

OK

cis                                central                      cis-central                                        Development   c811232a-4e80-4847-9888-a938ab3bac95   subaccount    ELASTIC_SERVICE           us10     OK      Succeeded to update assignment of service plan.   
➜  task8 git:(main) ✗ 
</pre>

Now we have the Entitlement, this is an "always free" service [discovery center](https://discovery-center.cloud.sap/serviceCatalog/cloud-management-service?region=all).

<pre>
➜  task8 git:(main) ✗ cf create-service cis central cis
Creating service instance cis in org John Astill_development-hkas66x8 / space dev as john_sap@astill.org...

Service instance cis created.
OK

➜  task8 git:(main) ✗ 
</pre>

List the services

<pre>
➜  task8 git:(main) ✗ cf services
Getting service instances in org John Astill_development-hkas66x8 / space dev as john_sap@astill.org...

name   offering   plan      bound apps   last operation     broker                                        upgrade available
cis    cis        central                create succeeded   sm-cis-1ddf6d79-a8ab-42a8-8c2a-f0c51e81bb54   no
➜  task8 git:(main) ✗ 
</pre>

Now to create a service key

<pre>
➜  task8 git:(main) ✗ cf csk cis cis_key
Creating service key cis_key for service instance cis as john_sap@astill.org...
OK

➜  task8 git:(main) ✗ 
</pre>

Now view the service key..

<pre>
cf service-key cis cis_key

....
</pre>

Hmm expected to have to use authentication 

<pre>
➜  task8 git:(main) ✗ cf curl "/v2/service_instances"
{
  "total_results": 1,
  "total_pages": 1,
  "prev_url": null,
  "next_url": null,
  "resources": [
    {
      "metadata": {
        "guid": "7f7b93d8-d7f6-452b-bc0b-50fe7572605e",
        "url": "/v2/service_instances/7f7b93d8-d7f6-452b-bc0b-50fe7572605e",
        "created_at": "2023-08-29T03:05:54Z",
        "updated_at": "2023-08-29T03:05:55Z"
      },
      "entity": {
        "name": "cis",
        "credentials": {},
        "service_plan_guid": "7cc70093-3c5f-47f2-acf6-8de4185ba63c",
        "space_guid": "26e1dcbc-0f55-422b-b5ec-3c632ee01bad",
        "gateway_data": null,
        "dashboard_url": null,
        "type": "managed_service_instance",
        "last_operation": {
          "type": "create",
          "state": "succeeded",
          "description": "",
          "updated_at": "2023-08-29T03:05:55Z",
          "created_at": "2023-08-29T03:05:55Z"
        },
        "tags": [],
        "maintenance_info": {},
        "service_guid": "4eacd0ef-9a9d-4cb3-8fb1-60fb685d8f82",
        "space_url": "/v2/spaces/26e1dcbc-0f55-422b-b5ec-3c632ee01bad",
        "service_plan_url": "/v2/service_plans/7cc70093-3c5f-47f2-acf6-8de4185ba63c",
        "service_bindings_url": "/v2/service_instances/7f7b93d8-d7f6-452b-bc0b-50fe7572605e/service_bindings",
        "service_keys_url": "/v2/service_instances/7f7b93d8-d7f6-452b-bc0b-50fe7572605e/service_keys",
        "routes_url": "/v2/service_instances/7f7b93d8-d7f6-452b-bc0b-50fe7572605e/routes",
        "service_url": "/v2/services/4eacd0ef-9a9d-4cb3-8fb1-60fb685d8f82",
        "shared_from_url": "/v2/service_instances/7f7b93d8-d7f6-452b-bc0b-50fe7572605e/shared_from",
        "shared_to_url": "/v2/service_instances/7f7b93d8-d7f6-452b-bc0b-50fe7572605e/shared_to",
        "service_instance_parameters_url": "/v2/service_instances/7f7b93d8-d7f6-452b-bc0b-50fe7572605e/parameters"
      }
    }
  ]
}
➜  task8 git:(main) ✗ 
</pre>