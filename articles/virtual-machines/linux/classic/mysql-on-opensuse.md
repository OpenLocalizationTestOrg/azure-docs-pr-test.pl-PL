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
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a>Instalowanie bazy danych MySQL na maszynie wirtualnej z dystrybucją systemu OpenSUSE Linux na platformie Azure
[MySQL] [ MySQL] popularnych, open source baza danych SQL. W tym samouczku przedstawiono sposób toocreate maszyny wirtualnej z systemem OpenSUSE Linux, następnie zainstalować MySQL.

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a>Utwórz maszynę wirtualną z systemem OpenSUSE Linux
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a>Zainstalować i uruchomić na maszynie wirtualnej hello MySQL
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o MySQL, zobacz hello [dokumentacji MySQL][MySQLDocs].

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

