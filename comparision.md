# Vault vs. Other Secret Management Services

### Vault vs. AWS Secret Manager
[Reddit Post](https://www.reddit.com/r/devops/comments/8zmibk/aws_secrets_manager_vs_hashicorp_vault_what_can/)

There's a massive difference between Vault and AWS Secrets Manager.

ASM is an AWS native way of storing secure static K/V pairs. It does have some rotation ability, but outside of RDS, you essentially have to write those functions on your own. Also, ASM is single region only.

Vault has the following

Secure K/V Store

Cubbyholes where only the token bearer can access the data. Not even system/Vault administrators can access them.

Dynamic secrets. Vault will create accounts and credentials for you in databases and cloud IAMs. You can also tie these to highly configurable leases and access policies. Want to grant someone read-only access to your Cloudwatch for 10 minutes and have those keys automatically removed from the system when those 10 minutes are up? This is a way.

PKI engine to do one click/API call certificate generation. Also with highly configurable TTLs (I've used 1 minute with success in demos/webinars)

SSH CA authority. Similar to PKI but for signing SSH certs. Of course, with highly configurable TTLs. Want to let someone logon to a set of servers for 5 minutes without managing their keys on the servers? This is the way.

Encryption as a Service/Transit. Encrypt all payloads for your applications via simple API calls. Includes versioning and encryption rollover methods. Great for encrypting at-rest data in any storage backend (database, block store, disk, etc).

Cross region/Cross Cloud/Cross Datacenter replication.

Mount Filters to restrict data that should not be transferred across clusters. Great for GDPR use cases.

Control Groups to only allow access to secrets after N approvals have been met.

Sentinel Policy as Code for highly configurable access rules based on metadata (e.g. only allow access to a set of secrets from 10AM-6PM if requests come from 192.168.42.0/24)

All major authentication methods and optional MFA.

Pluggable architecture.

Instant synergies with Terraform, Nomad and Consul

Cloud agnostic. You can run it anywhere, laptop, on-prem datacenter, AWS, Azure, GCP, Alibaba...etc.

Now, all that being said, if you're looking for a managed service and simple secure K/V storage, Vault may not be for you.

** I'm a HashiCorp Employee **
