# Create a simple lab environment to test hybrid authentication features with Azure AD. 


This template will deploy a set of Windows Server 2012R2, 2016, 2019 or 2022 VMs that can be used as an Azure AD single sign-on lab.


<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fliodiera%2freprolab%2fmaster%2fazuredeploy.json" target="_blank">
    <img src="https://aka.ms/deploytoazurebutton"/>
</a>
<a href="http://armviz.io/#/?load=https%3a%2f%2fraw.githubusercontent.com%2fliodiera%2freprolab%2fmaster%2fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

## Networking

The virtual network has two subnets:  an external-facing subnet an an internal subnet.  A network security group on the internal subnet prevents all inbound traffic and only allows ports 53, 443, and 3389 from the external subnet. A network security group on the external subnet restricts ports 3389, 443, and 49443 to the Gateway VM from the public IP address specified in the template. 

## VMs

This template deploys the following VMs in the specified subnet. You will be able to remote into all VMs from the remote desktop jump server.
<ol>
<li>Remote desktop jump server/ADFS Proxy server (external)</li>
<li>Domain controller (internal)</li>
<li>ADFS farm server (internal)</li>
<li>Synchronization server (internal)</li>
</ol>

With the exception of the domain controller, the template only deploys the operating system to the VMs and joins them to the domain.

## Active Directory Domain Services

This template also deploys and configures an AD DS single-domain forest and populates the domain with generic OUs, users, and groups.  All of the VMs on the internal subnet are joined to this domain.

Template based on mbakunas/azure-ad-sso-lab and dakoer/Synlab
