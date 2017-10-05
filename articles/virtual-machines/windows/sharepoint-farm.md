---
title: "Tworzenie farmy serwerów programu SharePoint na platformie Azure | Dokumentacja firmy Microsoft"
description: "Szybko utworzyć nową farmę programu SharePoint 2013 lub SharePoint 2016 na platformie Azure przy użyciu witrynę portalu Azure marketplace."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 00648ee35962b22fb7eeceaa6d9df7305c801abf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-sharepoint-server-farms-using-the-azure-portal-marketplace"></a>Tworzenie farmy serwerów programu SharePoint przy użyciu witrynę portalu Azure marketplace

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>Farm programu SharePoint 2013
Microsoft Azure Marketplace portalu można szybko utworzyć wstępnie skonfigurowane farm programu SharePoint Server 2013. To można zaoszczędzić dużo czasu na potrzeby farmy programu SharePoint podstawowego lub wysokiej dostępności dla środowiska i testowania lub jeśli dokonujesz oceny programu SharePoint Server 2013 jako rozwiązanie współpracy dla Twojej organizacji.

> [!NOTE]
> **Farmy serwerów programu SharePoint** usunięto element w portalu Azure Marketplace w portalu Azure. Zostało zastąpione przez **farmy SharePoint 2013 nie - HA** i **farmy programu SharePoint 2013 HA** elementów.
>
>

Podstawowe farmy programu SharePoint obejmuje trzy maszyny wirtualne w tej konfiguracji.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

Uproszczona konfiguracja do tworzenia aplikacji programu SharePoint lub ocenę pierwszego programu SharePoint 2013, można użyć tej konfiguracji farmy.

Aby utworzyć podstawowy farmy programu SharePoint (trzech serwerów):

1. Kliknij przycisk [tutaj](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).
2. Kliknij przycisk **wdrażanie**.
3. Na **farmy SharePoint 2013 nie - HA** okienku, kliknij przycisk **Utwórz**.
4. Określ ustawienia na kroki **tworzenia farmy SharePoint 2013 nie - HA** okienka, a następnie kliknij przycisk **Utwórz**.

Farma programu SharePoint wysokiej dostępności składa się z dziewięciu maszyn wirtualnych w tej konfiguracji.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

Tej konfiguracji farmy służy do testowania wyższej klienta obciążenia, wysoką dostępność zewnętrznej witryny programu SharePoint i grup dostępności AlwaysOn programu SQL Server dla farmy programu SharePoint. Ta konfiguracja służy także do tworzenia aplikacji programu SharePoint w środowisku o wysokiej dostępności.

Aby utworzyć farmę programu SharePoint (serwerze 9) wysokiej dostępności:

1. Kliknij przycisk [tutaj](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).
2. Kliknij przycisk **wdrażanie**.
3. Na **farmy programu SharePoint 2013 HA** okienku, kliknij przycisk **Utwórz**.
4. Określ ustawienia na siedem kroków **tworzenia farmy programu SharePoint 2013 HA** okienka, a następnie kliknij przycisk **Utwórz**.

> [!NOTE]
> Nie można utworzyć **farmy SharePoint 2013 nie - HA** lub **farmy programu SharePoint 2013 HA** z bezpłatnej wersji próbnej platformy Azure.
>
>

Azure portal tworzy oba te farm tylko w chmurze sieci wirtualnej internetowy witrynę internetową. Brak połączenia lokacja lokacja sieci VPN i ExpressRoute do sieci organizacji.

> [!NOTE]
> Podczas tworzenia podstawowego lub farmy programu SharePoint wysokiej dostępności przy użyciu portalu Azure, nie można określić istniejącą grupę zasobów. Aby obejść to ograniczenie, Utwórz te farm przy użyciu programu Azure PowerShell. Aby uzyskać więcej informacji, zobacz [tworzenie programu SharePoint 2013: tworzenie i testowanie farm przy użyciu programu Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>Farm programu SharePoint 2016
Zobacz [w tym artykule](https://technet.microsoft.com/library/mt723354.aspx) instrukcje dotyczące kompilacji następujące farmy programu SharePoint Server 2016 pojedynczego serwera.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-the-sharepoint-farms"></a>Zarządzanie farmy programu SharePoint
Serwery te farm za pomocą połączenia pulpitu zdalnego można administrować. Aby uzyskać więcej informacji, zobacz [Zaloguj się do maszyny wirtualnej](quick-create-portal.md#connect-to-virtual-machine).

Z lokacji centralnej administracji programu SharePoint można skonfigurować Moje witryny, aplikacji programu SharePoint i innych funkcji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie programu SharePoint](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Następne kroki
* Odnajdywanie dodatkowe [konfiguracji programu SharePoint](https://technet.microsoft.com/library/dn635309.aspx) w usług infrastruktury platformy Azure.
