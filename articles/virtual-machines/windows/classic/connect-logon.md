---
title: aaaLog na tooa klasyczne maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Użyj hello toolog portalu Azure na maszynie wirtualnej Windows tooa utworzone za pomocą hello klasycznego modelu wdrażania."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a>Zaloguj się na tooa maszyny wirtualnej systemu Windows przy użyciu hello portalu Azure
W portalu Azure hello, użyj hello **Connect** przycisk toostart sesję pulpitu zdalnego i zaloguj się na tooa maszyny Wirtualnej systemu Windows.

Czy chcesz tooa tooconnect maszyny Wirtualnej systemu Linux Zobacz [jak toolog na tooa maszyny wirtualnej z systemem Linux](../../linux/mac-create-ssh-keys.md).

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Aby dowiedzieć się, jak toolog na tooa maszynę Wirtualną przy użyciu hello Resource Manager modelu, zobacz [tutaj](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="connect-toohello-virtual-machine"></a>Połącz toohello maszyny wirtualnej
1. Zaloguj się toohello portalu Azure.
2. Polecenie hello maszyny wirtualnej, które mają tooaccess. Nazwa Hello jest wyświetlana w hello **wszystkie zasoby** okienka.

    ![Lokalizacje wirtualne — komputera](./media/connect-logon/azureportaldashboard.png)

3. Kliknij przycisk **Connect** na pasku poleceń hello nad hello maszyny wirtualnej z pulpitu nawigacyjnego.

    ![Połączenia dla maszyny wirtualnej hello](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a>Zaloguj się na maszynie wirtualnej toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Następne kroki
* Jeśli hello **Connect** przycisk jest nieaktywny lub występują inne problemy z połączeniem pulpitu zdalnego hello, spróbuj zresetować hello konfiguracji. Kliknij przycisk **Zresetuj dostęp zdalny** z poziomu pulpitu nawigacyjnego hello maszyny wirtualnej.

    ![Resetowanie zdalnego dostępu](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* Problemy z hasłem spróbuj zresetować urządzenie. Kliknij przycisk **resetowania hasła** wzdłuż hello lewej krawędzi pulpitu nawigacyjnego maszyny wirtualnej, w obszarze **pomocy technicznej i rozwiązywania problemów**.

    ![Zresetuj hasło](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

Te porady nie działa lub nie są potrzebne, zobacz [tooa połączeń pulpitu zdalnego Rozwiązywanie problemów z maszyny wirtualnej z systemem Windows Azure](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). W tym artykule przedstawiono sposób diagnozowania i rozwiązywania typowych problemów.
