---
title: "Artykuły techniczne dla klasycznych maszyn wirtualnych systemu Windows | Microsoft Azure"
description: "Pełna lista artykuły dokumentacji Microsoft Azure dla maszyn wirtualnych systemu Windows w klasycznym modelu wdrażania"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-service-management
editor: 
ms.assetid: 7f9a508b-34ec-4bdb-92d1-8844480369d5
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: danlep
ms.openlocfilehash: 2df7ea6a143ad0d64e4fd75223c7e5a9a2a5e87e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="technical-articles-for-windows-vms-in-the-classic-deployment-model"></a>Artykuły techniczne dla maszyn wirtualnych systemu Windows w klasycznym modelu wdrażania
Znajdź wszystkie dokumentacji potrzebnych do tworzenia i zarządzania systemem Windows Azure maszyny wirtualne w klasycznym modelu wdrażania.

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia. Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.

## <a name="overview"></a>Omówienie
[Informacje o maszynach wirtualnych](windows/overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Często zadawane pytania dotyczące maszyn wirtualnych Azure utworzonych za pomocą klasycznym modelu wdrażania](windows/classic/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Porównanie maszyn wirtualnych, witryn sieci Web i usług w chmurze](../app-service-web/choose-web-site-cloud-service-vm.md)

[Maszyny wirtualne i kontenerów na platformie Azure](windows/containers.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="environment-setup"></a>Konfiguracja środowiska
[Bezpłatne konto](https://azure.microsoft.com/free/)

[Instalowanie programu Azure PowerShell](/powershell/azure/overview)

[Instalowanie interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md)

## <a name="get-started"></a>Rozpoczęcie pracy
[Ścieżka szkoleniowa dotycząca maszyn wirtualnych systemu Windows](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)

[Utwórz maszynę wirtualną systemu Windows w klasycznym portalu Azure](windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Jak zalogować się do klasycznego maszynę wirtualną z systemem Windows Server](windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="plan"></a>Planowanie
[Informacje o obrazach klasycznych maszyn wirtualnych](windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Rozmiary maszyn wirtualnych](windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Rozmiary maszyn wirtualnych wysokiej wydajności obliczeniowej](windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Planowana konserwacja maszyn wirtualnych platformy Azure](windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Wytyczne dotyczące implementacji usług infrastruktury platformy Azure](windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Utwórz zbiór dostępności dla maszyn wirtualnych](windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="deploy"></a>Wdrażanie
[Utwórz niestandardowe maszynę wirtualną z systemem Windows](windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Przechwytywanie maszyny wirtualnej systemu Windows tworzone w klasycznym modelu wdrażania](windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Tworzenie i przekazywanie klasycznego VHD serwera z systemem Windows przy użyciu programu PowerShell](windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Automatyzacja wdrażania maszyny wirtualnej platformy Azure z Chef](windows/chef-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Tworzenie i konfigurowanie programu Azure PowerShell klasyczne maszyny wirtualnej systemu Windows](windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Wstrzykiwania niestandardowe dane do maszyny wirtualnej platformy Azure](windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="manage"></a>Zarządzanie
[Zarządzanie maszyn wirtualnych przy użyciu programu Azure PowerShell](windows/classic/manage-psh.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Klasyczne sieci wirtualne nawiązać połączenia z nowej sieci wirtualnych](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)

[Dotyczące agenta maszyny wirtualnej i rozszerzeń](windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Zarządzaj rozszerzeniami maszyny wirtualnej](windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Niestandardowe rozszerzenie skryptu klasycznych maszyn wirtualnych systemu Windows](windows/classic/extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Platforma obsługiwana migracja z klasycznego do usługi Azure Resource Manager](windows/migration-classic-resource-manager-deep-dive.md)

## <a name="configure"></a>Konfigurowanie
[Jak można zresetować hasło lub usługa Pulpit zdalny dla maszyny Wirtualnej systemu Windows](windows/reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Temat funkcji i rozszerzeń maszyny wirtualnej](windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Jak zainstalować i skonfigurować Symantec Endpoint Protection na maszynie Wirtualnej systemu Windows](windows/classic/install-symantec.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Jak zainstalować i skonfigurować Trend Micro głębokie zabezpieczeń jako usługa na maszynie Wirtualnej systemu Windows](windows/classic/install-trend.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Jak skonfigurować zbiór dostępności dla maszyn wirtualnych w klasycznym modelu wdrażania](windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Jak skonfigurować punkty końcowe na maszynie wirtualnej Azure classic](windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a>Magazyn
[O dyskach i wirtualne dyski twarde dla maszyn wirtualnych platformy Azure](../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Jak można dołączyć dysku danych do klasycznej maszyny wirtualnej systemu Windows](windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Jak można odłączyć dysku danych od klasyczne maszyny wirtualnej systemu Windows](windows/classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Użyj dysku D jako dysk z danymi na maszynie Wirtualnej systemu Windows](windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="networking"></a>Sieć
[Omówienie sieci wirtualnej](../virtual-network/virtual-networks-overview.md)

[Połączenie maszyn wirtualnych utworzonych za pomocą klasycznego modelu wdrażania z wirtualnych sieci lub usługę w chmurze](windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Zarządzanie sieciowymi grupami zabezpieczeń przy użyciu programu Azure PowerShell](../virtual-network/virtual-networks-create-nsg-classic-ps.md)

[Tworzenie modułu równoważenia obciążenia](../load-balancer/load-balancer-get-started-internet-classic-portal.md)

## <a name="develop"></a>Programowanie
[Tworzenie i zarządzanie nimi maszyn wirtualnych platformy Azure w programie Visual Studio](windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Tworzenie maszyny wirtualnej dla aplikacji sieci web za pomocą programu Visual Studio](windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Jak uruchomić zadanie obliczeniowych w języku Java na maszynie wirtualnej](windows/classic/java-run-compute-intensive-task.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Aplikacja sieci web Django Hello World na maszynie Wirtualnej systemu Windows Server](windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="workloads"></a>Obciążenia
[HPC Pack](windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[MongoDB](windows/classic/install-mongodb.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[MySQL](windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Oracle](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html#support)

[SAP](windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[SQL Server](./windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[Tomcat](windows/classic/java-run-tomcat-app-server.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="reference"></a>Dokumentacja
[Azure polecenia interfejsu wiersza polecenia w trybie zarządzania usługami](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)

[Interfejs API REST zarządzania usługami](https://msdn.microsoft.com/library/azure/ee460799.aspx)

[Zarządzanie usługami interfejs API .NET](https://msdn.microsoft.com/library/azure/mt420161.aspx)

[Azure dokumentacji polecenia cmdlet programu PowerShell do zarządzania usługi](/powershell/azure/overview?view=azuresmps-3.7.0)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[Rozwiązywanie problemów z połączeniami pulpitu zdalnego nawiązywanymi z maszyną wirtualną platformy Azure z systemem Windows](windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Rozwiązywanie problemów z dostępem do aplikacji działających na maszynie wirtualnej platformy Azure](windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Rozwiązywanie problemów z przydziałem podczas tworzenia, uruchom ponownie lub zmień rozmiar maszyn wirtualnych na platformie Azure](windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Rozwiązywanie problemów wdrożenie klasyczne z Tworzenie nowej maszyny wirtualnej systemu Windows na platformie Azure](windows/classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[Rozwiązywanie problemów wdrożenie klasyczne z ponownego uruchamiania lub zmiana rozmiaru istniejącej maszyny wirtualnej systemu Windows na platformie Azure](windows/classic/virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
