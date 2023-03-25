# Monitoring and Management

## Governance

### Azure Policy
Governance validates that your organization can achieve its goals through effective and efficient us of IT. 
The plocies are set of rules.

### Role-Based Access Control (RBAC)
- **Define user access**: You can define specific user access to individual resources.
- **Minimum access**: RBAC enable minimum access necessary to resources. This ensures only users with valid access can manage resources.
- **Target specifc use cases**: Be very explicit about uses and access. For example, allow an application access to certain resources or allow a user to manage resources in a resource group.

![image](https://user-images.githubusercontent.com/48266482/227698157-630c3ef4-cf7c-45ed-932e-e8edd8a2c19e.png)

![image](https://user-images.githubusercontent.com/48266482/227698177-3041ff0d-122b-44a8-8bbf-8f9360af4630.png)

### Locks
- **Assigning**: Assign a lock to a subscription, resource group or resource.
- **Types**: A lock can be of two types. Delete where you can't delete the locked object. Read-Only, where you can't make any changes to the object.
- **Locked means locked**: A lock needs to be removed before the locked actions can be performed again.

### Azure Blueprints
Blueprints are templates for creating Azure resources.

![image](https://user-images.githubusercontent.com/48266482/227698362-15b520fc-f874-482f-87ca-e0695e40db15.png)

### Cloud adoption framework
- **Collection of Documents**: Lots of resources to guide you through the cloud adoption process.
- **Guidance**: Help to define strategies for adoption, planning the move, "being ready" for the cloud, adoption reason, governance practices, and managing a living, breathing cloud architecture.
- **Governance**: Key to the cloud adoption process is governance of the process. The Cloud Adoption Framework is a big step in that process.

### Exam tips:
Governance keeps you compliant and out of trouble.

- Azure Policy ensures that policies applied to resources are compliant.
- A policy is a set of rules to ensure compliant resources.
- Role Based Access Control (RBAC) ensures user compliance through assigning a role to a user. A role is a combination of security principal, role definition and scope.
- Locks make sure that subscriptions, resource groups or resources are either not modified or not deleted.
- Blueprints are templates for creating standard Azure environments.
- The Azure Advisor for Security Assistance is part of the Security Center.

## Azure Monitor

## Azure Service Health

## Compliance

## Privacy

## Trust

## Azure Arc
