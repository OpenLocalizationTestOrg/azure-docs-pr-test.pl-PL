---
title: aaaInstall MongoDB na maszynie Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall MongoDB na maszynie Wirtualnej platformy Azure utworzona z hello klasycznego modelu wdrażania systemem Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Instalowanie bazy danych MongoDB Windows maszyny Wirtualnej na platformie Azure
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. tooinstall oraz konfigurowania bazy danych MongoDB przy użyciu modelu wdrażania usługi Resource Manager hello, zobacz [w tym artykule](../install-mongodb.md).

[Bazy danych MongoDB] [ MongoDB] jest popularnych open source, wysokiej wydajności bazę danych NoSQL. W tym artykule prowadzi użytkownika przez proces tworzenia maszyny wirtualnej systemu Windows Server (VM) przy użyciu hello [portalu Azure][AzurePortal]. Następnie utwórz i Dołącz toohello dysku danych maszyny Wirtualnej przed zainstalowaniem i skonfigurowaniem bazy danych MongoDB. Jeśli masz istniejącą maszynę Wirtualną na platformie Azure, które chcesz toouse, można przejść bezpośrednio za[Instalowanie i Konfigurowanie bazy danych MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Tworzenie maszyny wirtualnej z systemem Windows Server
Wykonaj te instrukcje toocreate maszyny wirtualnej.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> Dodawanie punktu końcowego dla bazy danych MongoDB podczas tworzenia maszyny wirtualnej hello i skonfigurować w następujący sposób: go jako nazwa **Mongo**, użyj **TCP** jako protokół hello i ustaw zarówno hello portów publicznego i prywatnego zbyt**27017**.
>
>

## <a name="attach-a-data-disk"></a>Dołączanie dysku danych
Magazyn tooprovide hello maszyny wirtualnej, dołączenie dysku danych i zainicjować go, aby można go używać systemu Windows. Jeśli masz już dysk danych, można dołączyć istniejącego dysku, lub możesz dołączyć pusty dysk.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

Aby uzyskać instrukcje na inicjowanie dysku hello, zobacz "jak: Zainicjuj nowy dysk danych w systemie Windows Server" w [jak tooattach danych na dysku maszyny wirtualnej systemu Windows tooa](attach-disk.md).

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>Zainstalować i uruchomić na maszynie wirtualnej hello bazy danych MongoDB
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Podsumowanie
W tym samouczku przedstawiono sposób toocreate maszyny wirtualnej z systemem Windows Server zdalnie połączyć tooit i dołączenie dysku danych.  Przedstawiono również sposób tooinstall i konfigurowanie maszyny wirtualnej z systemem Windows hello bazy danych MongoDB. Można uzyskać dostęp bazy danych MongoDB hello systemu Windows maszyny wirtualnej przez następujące hello zaawansowanych tematów w hello [dokumentacją usługi MongoDB][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

