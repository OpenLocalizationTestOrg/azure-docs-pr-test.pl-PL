---
title: "aaaCreate farmy serwerów programu SharePoint na platformie Azure | Dokumentacja firmy Microsoft"
description: "Szybko utworzyć nową farmę programu SharePoint 2013 lub SharePoint 2016 na platformie Azure przy użyciu hello Azure portalu marketplace."
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
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>Tworzenie farmy serwerów programu SharePoint przy użyciu hello Azure portalu marketplace

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>Farm programu SharePoint 2013
Microsoft Azure hello portalu Marketplace można szybko utworzyć wstępnie skonfigurowane farm programu SharePoint Server 2013. To można zaoszczędzić dużo czasu na potrzeby farmy programu SharePoint podstawowego lub wysokiej dostępności dla środowiska i testowania lub jeśli dokonujesz oceny programu SharePoint Server 2013 jako rozwiązanie współpracy dla Twojej organizacji.

> [!NOTE]
> Witaj **farmy serwerów programu SharePoint** usunięto element w portalu Azure Marketplace hello hello portalu Azure. Zastąpiono z hello **farmy SharePoint 2013 nie - HA** i **farmy programu SharePoint 2013 HA** elementów.
>
>

Hello podstawowego farmy programu SharePoint obejmuje trzy maszyny wirtualne w tej konfiguracji.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

Uproszczona konfiguracja do tworzenia aplikacji programu SharePoint lub ocenę pierwszego programu SharePoint 2013, można użyć tej konfiguracji farmy.

toocreate hello podstawowe (farmy trzech serwerów) programu SharePoint:

1. Kliknij przycisk [tutaj](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).
2. Kliknij przycisk **wdrażanie**.
3. Na powitania **farmy SharePoint 2013 nie - HA** okienku, kliknij przycisk **Utwórz**.
4. Określ ustawienia na powitania kroki hello **tworzenia farmy SharePoint 2013 nie - HA** okienka, a następnie kliknij przycisk **Utwórz**.

farma programu SharePoint wysokiej dostępności Hello składa się z dziewięciu maszyn wirtualnych w tej konfiguracji.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

Można użyć tej farmy konfiguracji tootest wyższe klienta obciążeniem, wysoką dostępność hello zewnętrznej witryny programu SharePoint i grup dostępności AlwaysOn programu SQL Server dla farmy programu SharePoint. Ta konfiguracja służy także do tworzenia aplikacji programu SharePoint w środowisku o wysokiej dostępności.

farma programu SharePoint toocreate hello wysokiej dostępności (9 serwerów):

1. Kliknij przycisk [tutaj](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).
2. Kliknij przycisk **wdrażanie**.
3. Na powitania **farmy programu SharePoint 2013 HA** okienku, kliknij przycisk **Utwórz**.
4. Określ ustawienia na powitania siedmiu kroków hello **tworzenia farmy programu SharePoint 2013 HA** okienka, a następnie kliknij przycisk **Utwórz**.

> [!NOTE]
> Nie można utworzyć hello **farmy SharePoint 2013 nie - HA** lub **farmy programu SharePoint 2013 HA** z bezpłatnej wersji próbnej platformy Azure.
>
>

Witaj portalu Azure tworzy oba te farm tylko w chmurze sieci wirtualnej internetowy witrynę internetową. Nie jest żadna lokacja lokacja sieci VPN i ExpressRoute połączenia wstecz tooyour organizacji sieć.

> [!NOTE]
> Po hello tworzenia podstawowego lub farmy programu SharePoint wysokiej dostępności przy użyciu hello portalu Azure, nie można określić istniejącą grupę zasobów. toowork wokół to ograniczenie, Utwórz te farm przy użyciu programu Azure PowerShell. Aby uzyskać więcej informacji, zobacz [tworzenie programu SharePoint 2013: tworzenie i testowanie farm przy użyciu programu Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>Farm programu SharePoint 2016
Zobacz [w tym artykule](https://technet.microsoft.com/library/mt723354.aspx) dla hello toobuild instrukcje powitania po jednym serwerze programu SharePoint Server 2016 farmy.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>Zarządzanie hello farmy programu SharePoint
Można administrować serwerami hello tych farm za pomocą połączenia pulpitu zdalnego. Aby uzyskać więcej informacji, zobacz [Zaloguj się na maszynie wirtualnej toohello](quick-create-portal.md#connect-to-virtual-machine).

Z lokacji centralnej administracji programu SharePoint hello można skonfigurować Moje witryny, aplikacji programu SharePoint i innych funkcji. Aby uzyskać więcej informacji, zobacz [Konfigurowanie programu SharePoint](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Następne kroki
* Odnajdywanie dodatkowe [konfiguracji programu SharePoint](https://technet.microsoft.com/library/dn635309.aspx) w usług infrastruktury platformy Azure.
