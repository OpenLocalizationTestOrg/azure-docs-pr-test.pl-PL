---
title: aaaInstall bazy danych MySQL na maszynie Wirtualnej platformy OpenSUSE | Dokumentacja firmy Microsoft
description: "Dowiedz się tooinstall MySQL na komputerze OpenSUSE VMirtual systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="ed55e-103">Instalowanie bazy danych MySQL na maszynie wirtualnej z dystrybucją systemu OpenSUSE Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ed55e-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="ed55e-104">[MySQL] [ MySQL] popularnych, open source baza danych SQL.</span><span class="sxs-lookup"><span data-stu-id="ed55e-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="ed55e-105">W tym samouczku przedstawiono sposób toocreate maszyny wirtualnej z systemem OpenSUSE Linux, następnie zainstalować MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed55e-105">This tutorial shows you how toocreate a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ed55e-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ed55e-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ed55e-107">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="ed55e-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ed55e-108">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ed55e-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="ed55e-109">Utwórz maszynę wirtualną z systemem OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="ed55e-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a><span data-ttu-id="ed55e-110">Zainstalować i uruchomić na maszynie wirtualnej hello MySQL</span><span class="sxs-lookup"><span data-stu-id="ed55e-110">Install and run MySQL on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="ed55e-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ed55e-111">Next steps</span></span>
<span data-ttu-id="ed55e-112">Aby uzyskać więcej informacji o MySQL, zobacz hello [dokumentacji MySQL][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="ed55e-112">For details about MySQL, see hello [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

