#如何为虚拟机附加磁盘

关于如何在门户网站上附加磁盘请阅读[这篇文章](http://www.windowsazure.cn/documentation/articles/storage-windows-attach-disk/)

>使用Powershell前有关Azure PowerShell的安装、配置和连接到订阅请阅读[这篇文章](http://www.windowsazure.cn/documentation/articles/powershell-install-configure)

相关PowerShell指令：[Get-AzureDataDisk](https://msdn.microsoft.com/en-us/library/azure/dn495197.aspx)、[Add-AzureDataDisk](https://msdn.microsoft.com/en-us/library/azure/dn495298.aspx)、[Remove-AzureDataDisk](https://msdn.microsoft.com/en-us/library/azure/dn495243.aspx)

本文主要在虚拟机"pstest"上测试。

	#获取虚拟机上数据磁盘的详细信息
	$vm=Get-AzureVM -ServiceName 'pstest' -Name 'pstest'
	Get-AzureDataDisk -VM $vm

	#添加数据磁盘
	Add-AzureDataDisk -VM $vm -CreateNew -DiskSizeInGB 10 -DiskLabel 'movie' -LUN 1 -MediaLocation "https://portalvhdsw0kfpkwrwbyf2.blob.core.chinacloudapi.cn/vhds/pstest-pstest-0126-2.vhd" | Update-AzureVM

	Add-AzureDataDisk -VM $vm -CreateNew -DiskSizeInGB 10 -DiskLabel 'test' -LUN 0 -MediaLocation "https://portalvhdsw0kfpkwrwbyf2.blob.core.chinacloudapi.cn/vhds/pstest-sport1.vhd" | Update-AzureVM

	#移除数据磁盘
	Remove-AzureDataDisk -LUN 0 -VM $vm | Update-AzureVM

	#附加存在于Azure存储的数据磁盘
	Add-AzureDataDisk -VM $vm -CreateNew -DiskSizeInGB 10 -DiskLabel 'test' -LUN 0 -MediaLocation "https://portalvhdsw0kfpkwrwbyf2.blob.core.chinacloudapi.cn/vhds/pstest-sport1.vhd" | Update-AzureVM

**注意：**

- 附加磁盘不会引起虚拟机重启，也不需要虚拟机重启。
- 通过Remove-AzureDataDisk操作后vhd文件没有被删除，只是数据磁盘从虚拟机上移除掉。如果磁盘完全没有用处并希望避免不必要的费用请单独删除。
- 根据虚拟机的尺寸，附加磁盘的个数也不一样。具体尺寸对应的附加磁盘数量请阅读[这篇文章](http://www.windowsazure.cn/documentation/articles/virtual-machines-size-specs)



