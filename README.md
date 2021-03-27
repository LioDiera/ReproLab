# Create a simple Azure Active Directory single sign-on lab environment


This template will deploy a set of Windows Server 2012, 2012R2, 2016, or 2019 VMs that can be used as an Azure AD single sign-on lab.


<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fliodiera%2fsynclab%2fmaster%2fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3a%2f%2fraw.githubusercontent.com%2fliodiera%2fsynclab%2fmaster%2fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

## Networking

The virtual network has two subnets:  an external-facing subnet an an internal subnet.  A network security group on the internal subnet prevents all inbound traffic and only allows 53, 443, and 3389 from the external subnet.

## VMs

This template deploys the following VMs (in the specified subnet):
<ol>
<li>Remote desktop jump server (external)</li>
<li>Domain controller (internal)</li>
<li>ADFS farm server (internal)</li>
<li>ADFS proxy server (external)</li>
<li>Synchronization server (internal)</li>
</ol>

With the exception of the domain controller the template only deploys the operating system to the VMs.

## Active Directory Domain Services

This template also deploys and configures an AD DS single-domain forest and populates the domain with OUs, users, and groups.  All of the VMs on the internal subnet are joined to this domain.

Template based on mbakunas/azure-ad-sso-lab and dakoer/Synlab