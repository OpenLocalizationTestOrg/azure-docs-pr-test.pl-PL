---
title: "aaaManage DNS strefy w usłudze Azure DNS - portalu Azure | Dokumentacja firmy Microsoft"
description: "Można zarządzać za pomocą portalu Azure hello stref DNS. W tym artykule opisano sposób tooupdate, usunąć i utworzyć strefy DNS w usłudze Azure DNS"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>Jak toomanage strefy DNS w hello portalu Azure

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-dnszones-cli.md)

W tym artykule opisano, jak toomanage serwery DNS strefy za pomocą hello portalu Azure. Można również zarządzać stref DNS przy użyciu wieloplatformowych hello [interfejsu wiersza polecenia Azure](dns-operations-dnszones-cli.md) lub hello Azure [PowerShell](dns-operations-dnszones.md).

## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

1. Zaloguj się toohello portalu Azure
2. W menu centralnym hello, kliknij polecenie, a następnie kliknij przycisk **nowy > Sieć >** , a następnie kliknij przycisk **strefy DNS** bloku strefy DNS Utwórz hello tooopen.

    ![Strefa DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. Na powitania **strefy DNS Utwórz** bloku wprowadź hello następujące wartości, a następnie kliknij przycisk **Utwórz**:


   | **Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Nazwa**|contoso.com|Nazwa Hello hello strefy DNS|
   |**Subskrypcja**|[Twoja subskrypcja]|Wybierz strefę DNS subskrypcji toocreate hello w.|
   |**Grupa zasobów**|**Utwórz nową:** contosoDNSRG|Utwórz grupę zasobów. Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych. więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artykuł z omówieniem.|
   |**Lokalizacja**|Zachodnie stany USA||

> [!NOTE]
> Grupa zasobów Hello odwołuje się lokalizacji toohello hello grupy zasobów, a nie ma wpływu na powitania strefy DNS. Lokalizacja strefy DNS Hello jest zawsze "globalne" i nie jest wyświetlany.

## <a name="list-dns-zones"></a>Lista stref DNS

W portalu Azure hello kolejno zbyt**więcej usług** > **sieci** > **stref DNS**. Każdej strefy DNS jest jest własnych zasobów, informacje, takie jak liczba zestawów rekordów i serwery nazw są widoczne w tym widoku. Kolumna Hello **serwery nazw** nie występuje w hello widok domyślny, tooadd kliknij **kolumn**, wybierz pozycję **serwery nazw** i kliknij przycisk **gotowe**.

![Lista stref DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>Usuń strefę DNS

Przejdź tooa strefy DNS w portalu hello. Na powitania **strefy DNS** bloku, kliknij przycisk **Usuń strefę**. Jesteś zostanie wyświetlony monit o tooconfirm są pożądane strefy DNS hello toodelete. Usunięcie strefy DNS powoduje usunięcie wszystkich rekordów hello, które są zawarte w strefie hello.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toowork strefy DNS i rekordy odwiedzając [wprowadzenie do usługi Azure DNS przy użyciu portalu Azure hello](dns-getstarted-portal.md).
