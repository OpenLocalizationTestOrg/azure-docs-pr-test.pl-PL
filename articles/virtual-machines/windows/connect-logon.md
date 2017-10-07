---
title: tooa aaaConnect maszyny Wirtualnej systemu Windows Server | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconnect i logowanie przy użyciu maszyny Wirtualnej systemu Windows tooa hello Azure portal hello Resource Manager wdrażania modelu."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>Jak dziennika na tooan wirtualnej platformy Azure i tooconnect komputera systemu Windows
Użyjesz hello **Connect** przycisk hello Azure toostart portalu sesji pulpitu zdalnego (RDP) na pulpicie systemu Windows. Najpierw połącz toohello maszyny wirtualnej, a następnie zaloguj się na.

Jeśli próbujesz tooa tooconnect maszyny Wirtualnej systemu Windows z Mac, należy tooinstall klientem RDP dla komputerów Mac, takich jak [pulpitu zdalnego firmy Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).

## <a name="connect-toohello-virtual-machine"></a>Połącz toohello maszyny wirtualnej
1. Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com/).
2. W menu Centrum powitania kliknij **maszyn wirtualnych**.
3. Wybierz maszynę wirtualną hello z listy hello.
4. W bloku hello hello maszyny wirtualnej, kliknij **Connect**.
   
    ![Zrzut ekranu przedstawiający portal Azure hello jak tooyour tooconnect maszyny Wirtualnej.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > Jeśli hello **Connect** przycisk w portalu hello jest nieaktywny i nie jesteś tooAzure połączonych za pośrednictwem [Express Route](../../expressroute/expressroute-introduction.md) lub [sieci VPN typu lokacja-lokacja](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) połączenia, należy toocreate i przypisać maszynie Wirtualnej publiczny adres IP, zanim będzie możliwe użycie protokołu RDP. Więcej informacji o [publicznych adresach IP na platformie Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Zaloguj się na maszynie wirtualnej toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Następne kroki
Jeśli wystąpiły problemy podczas próby tooconnect, zobacz [połączeń pulpitu zdalnego Rozwiązywanie problemów z](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). W tym artykule przedstawiono sposób diagnozowania i rozwiązywania typowych problemów.

