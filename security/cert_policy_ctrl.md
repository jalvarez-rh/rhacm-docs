# Certificate policy controller

Certificate policy controller can be used to detect certificates that are close to expiring. Configure and customize the certificate policy controller by updating the minimum duration parameter in your controller policy. When a certificate expires in less than the minimum duration amount of time, the policy becomes noncompliant. The certificate policy controller is created on your hub cluster.

The certificate policy controller communicates with the local Kubernetes API server to get the list of secrets that contain certificates and determine all non-compliant certificates. For more information about CRDs, see [Extend the Kubernetes API with CustomResourceDefinitions](https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/). 

Certificate policy controller does not support the `enforce` feature. 

## Certificate policy controller YAML structure

View the following example of a certificate policy and review the element in the YAML table:

  ```yaml
  APIVersion: policies.ibm.com/v1alpha1
  Kind: CertificatePolicy
  Metadata:
    Name: certificate-policy-example
    Namespace:
    Labels: category=system-and-information-integrity 
  Spec:
    NamespaceSelector:
      Exclude:
      Include:
    RemediationAction:
    Disabled:
    MinimumDuration:
  Status:
    CompliancyDetails:
      Certificate-Policy-Example:
        Default:
        Kube - Public:
    Compliant:
  Events:
  ```

### Certificate policy controller YAML table

|Field|Description|
|-- | -- |
| APIVersion | Required. Set the value to `policies.ibm.com/v1alpha1`. <!--current place holder until this info is updated--> |
| Kind | Required. Set the value to `CertificatePolicy` to indicate the type of policy. |
| Metadata.Name | Required. The name to identify the policy.|
| Metadata.Namespace | Required. The namespaces within the managed cluster where the policy is created. |
| Metadata.Labels | Optional. In a certificate policy, the `category=system-and-information-integrity` label categorizes the policy and facilitates querying the certificate policies. If there is a different value for the `category` key in your certificate policy, the value is overridden by the certificate controller. |
| Spec | Required. Specifications of which certificates to monitor and refresh.|
| Spec.NamespaceSelector| Required. Managed cluster namespace to which you want to apply the policy. Enter parameter values for `Include` and `Exclude`. **Note**: When you create multiple certificate policies and apply them to the same managed cluster, each policy `NamespaceSelector` must be assigned a different value.|
| Spec.RemediationAction | Required. Specifies the remediation of your policy. Set the parameter value to `inform`. Certificate policy controller only supports `inform` feature.|
| Spec.MinimumDuration | Required. parameter specifies the smallest duration (in hours) before a certificate is considered non-compliant. When the certificate expiration is greater than the `minimumDuration`, then the certificate is considered compliant. Default value is `100h`. The parameter value uses the time duration format from Golang. See [Golang Parse Duration](https://golang.org/pkg/time/#ParseDuration) for more information.| 
| Status | Output only. Information provided by the controller that shows the status of the policy.|
{: caption="Table 1. Required and optional definition fields, along with output parameters." caption-side="top"}


## Certificate policy sample

When your certificate policy controller is created on your hub cluster, a replicated policy is created on your managed cluster. Your certificate policy on your managed cluster might resemble the following file:

```yaml
apiVersion: policies.ibm.com/v1alpha1
kind: CertificatePolicy
metadata:
  name: certificate-policy-1
  namespace: kube-system
  label:
    category: "System-Integrity"
spec:
  namespaceSelector:
    include: ["default", "kube-*"]
    exclude: ["kube-system"]
  remediationAction: inform
  minimumDuration: 100h
```

Learn how to manage a certificate policy, see [Managing certificate policies](create_cert_pol.md) for more details. Refer to [Policy controllers](policy_controllers.md) for more topics.
