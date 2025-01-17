---
title: How to license Windows VMs using the UKCloud Key Management Server | UKCloud Ltd
description: Shows how to register virtual machines with the KMS within vCloud Director
services: vmware
author: Sue Highmoor
reviewer: Sue Highmoor
lastreviewed: 19/08/2019

toc_rootlink: How To
toc_sub1:
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: License Windows VMs using the UKCloud Key Management Server
toc_fullpath: How To/vmw-how-setup-kms.md
toc_mdlink: vmw-how-setup-kms.md
---

# How to license Windows VMs using the UKCloud Key Management Server

## Overview

You need to register the Windows virtual machines (VMs) that you create with the UKCloud Key Management Server (KMS). You need to set up a connection with the KMS to enable registration.

## Setting up a connection with the UKCloud KMS

Before product activation, make sure your VMs can communicate with the UKCloud KMS that exists outside your cloud organisation.

To allow this communication, you need to create a source network address translation (SNAT) and firewall rule on your edge gateway:

1. In vCloud Director, select the VDC for which server activation is required.

2. In the left navigation panel, click **Edges**.

    ![Edges menu option in vCloud Director](images/vmw-vcd91-mnu-edges.png)

3. Select the edge that you want to configure and click the **Configure Services** button.

    ![Configure Services button](images/vmw-vcd-edge-btn-config.png)

4. In the *Edge Gateway* dialog box, select the **NAT** tab and create a new SNAT rule.

5. Make sure that the **Applied On** field is set to reflect your network firewall tenant (NFT).

6. In the **Original Source IP/Range** field, enter the IP address, CIDR or range of addresses you want to SNAT out.

7. For the translated address, enter the external IP address of your edge gateway or one of your external IP address assignments.

    For more information about creating SNAT rules, see [*How to create NAT rules*](vmw-how-create-nat-rules.md).

8. Select the **Firewall** tab and make sure that an outbound rule exists on your firewall.

    Contact UKCloud Support for details of the **Destination IP** and **Destination Port**.

    For more information about creating firewall rules, see [*How to create firewall rules*](vmw-how-create-firewall-rules.md).

## Activating your Windows licence

1. Open a console to the VM you want to license and activate.

2. Launch a command line with administrator rights.

3. Enter:

        C:\ > slmgr /skms  kms.ukcloud.com:1688

4. You'll see the following pop-up box:

    ![Windows Script Host dialog box](images/vmw-windows-kms-activate.png)

5. If an error message appears indicating that the KMS server can't be contacted, it means either that the edge gateway hasn't been configured correctly or that DNS can't be retrieved. Try again by issuing the same command but using the IP address of the activation server:

        C:\ > slmgr /skms  <external IP address>:1688

    ![Windows Script Host dialog box](images/vmw-windows-kms-activate-ip.png)

6. Click **OK**, then from the same command line window, enter:

        C:\ >slmgr /ato

    ![Product successfully activated](images/vmw-windows-kms-activate-success.png)

## Related videos

- [*Licensing Windows VMs using the UKCloud Key Management Server video*](vmw-vid-licensing-kms.md)

## Feedback

If you find an issue with this article, click **Improve this Doc** to suggest a change. If you have an idea for how we could improve any of our services, visit the [Ideas](https://community.ukcloud.com/ideas) section of the [UKCloud Community](https://community.ukcloud.com).
