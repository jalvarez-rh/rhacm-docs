# Search in the console

For Red Hat Advanced Cluster Management for Kubernetes, Search provides visibility into your resources across all your clusters.

**Note:** You can type any text value in the _Search box_ and results include anything with that value from any property, such as a name or namespace. For example, if you search for `RedHat`, you can receive results such as `RedHat123`. 

For more specific search results, include the property in your search. For example, search for `name:RedHat` to search only in the `name` property.

1. Click **Search** in the navigation menu. 
2. Type a word in the _Search box_, then Search finds your resources that contain that value.
   
    - As you search for resources, you receive other resources that are related to your original search result, which help you visualize how the resources interact with other resources in the system. 
  
    - Search returns and lists each cluster with the resource that you search. For resources in the _hub_ cluster, the cluster name is displayed as _local-cluster_.
   
    - Your search results are grouped by `kind`, and each resource `kind` is grouped in a table. 

    - Your search options depend on your cluster objects. You can refine your results with specific labels. Search is case-sensitive when you query labels. See the following examples: name, namespace, status, and other resource fields. Auto-complete provides suggestions to refine your search. See the following example:

      - Search for a single field, such as `kind:pod` to find all pod resources.
      - Search for multiple fields, such as `kind:pod namespace:default` to find the pods in the default namespace. 
  
    **Notes:** 
  
    - Users are unable to search for values that contain an empty space. 

    - Any user can search for resources, but results are based on your role-based access control assignment. Additionally, if you save and share a Search query with another user, returned results depend on access level for that user. For more information on role access, see _Using RBAC Authorization_ in the [Kubernetes documentation](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

    - You can also search with conditions by using characters, such as `>, >=, <, <=, !=`.

      See the following example:

      - Search for `kind:pod status:!Running` to find all pod resources where the status is not `Running`.
      - Search for `kind:pod restarts:>1` to find all pods that restarted at least twice.

3. If you want to save your search, click the **Save disk** icon.  

