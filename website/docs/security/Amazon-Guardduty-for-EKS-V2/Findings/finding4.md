---
title: "Admin Access To Default ServiceAccount"
sidebar_position: 129
---


In this section we will grant admin privileges to the Default service account. This may result in pods unintentionally launched with admin privileges.This is not a best practice because pods get the Default service account's token. This will give unintentinalKubernetesadminstrative permissions to users who have access to exec into pods.

To simulate this we will need to bind clusterrole `cluster-admin` to a serviceaccount named `default`.

```bash
$ kubectl create rolebinding sa-default-admin --clusterrole=cluster-admin --serviceaccount=default:default --namespace=default
```

With in few minutes we will see the finding `Policy:Kubernetes/AdminAccessToDefaultServiceAccount` in guardduty portal.

![](policy_AdminAccessToDefaultServiceAccount.png)

Run the following command to delete the role binding.

Cleanup:

```bash
$ kubectl delete rolebinding sa-default-admin --namespace=default
```