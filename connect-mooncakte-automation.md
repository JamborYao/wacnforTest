#通过Azure Active Directory认证Azure 自动化服务

关于Azure 自动化的详细概念请阅读[这篇文章](http://www.windowsazure.cn/home/features/automation/)。

Azure自动化是通过Windows PowserShell工作流（也成为Runbook）来处理Azure的资源和第三方应用的创建、部署、监视和维护工作的。在执行Runbook的时候自然需要认证是否拥有合理的身份来执行操作。本文介绍如何通过Azure Active Directory来授权。

https://azure.microsoft.com/en-us/blog/getting-started-with-azure-automation-automation-assets-2/

https://azure.microsoft.com/en-us/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/

Get-AzureAutomationConnection -AutomationAccountName "jaauto" –ConnectionTypeName "Azure"

https://msdn.microsoft.com/en-us/library/dn921828.aspx

[Get-AzureAutomationCertificate](https://msdn.microsoft.com/en-us/library/dn913765.aspx)

	Get-AzureAutomationCertificate -AutomationAccountName "Contoso17"  

 Don’t enable multi-factor authentication. Multi-factor accounts cannot be used with Azure Automation.