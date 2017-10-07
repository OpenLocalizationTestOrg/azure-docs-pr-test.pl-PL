---
title: "wprowadzenie do usługi Azure DNS przy użyciu portalu Azure hello aaaGet | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate DNS strefy i rejestrowanie w usłudze Azure DNS. To jest toocreate przewodnik krok po kroku i zarządzanie pierwszą strefę DNS i rekordów przy użyciu hello portalu Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>Wprowadzenie do usługi Azure DNS przy użyciu hello portalu Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-getstarted-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-getstarted-cli.md)

W tym artykule przedstawiono toocreate kroki hello z pierwszą strefę DNS i rejestrowanie przy użyciu hello portalu Azure. Można również wykonywać te czynności przy użyciu programu Azure PowerShell lub hello wiersza polecenia platformy Azure i platform.

Strefa DNS jest rekordy DNS hello toohost używane dla określonej domeny. toostart hosting domeny w usłudze Azure DNS należy toocreate strefy DNS dla tej nazwy domeny. Każdy rekord DNS domeny zostanie utworzony w tej strefie DNS. Na koniec toopublish serwery DNS strefy toohello Internet, należy serwery nazw hello tooconfigure hello domeny. Każda z tych czynności opisano w hello następujące kroki.

## <a name="create-a-dns-zone"></a>Tworzenie strefy DNS

1. Zaloguj się toohello portalu Azure
2. W menu centralnym hello, kliknij polecenie, a następnie kliknij przycisk **nowy > Sieć >** , a następnie kliknij przycisk **strefy DNS** bloku strefy DNS Utwórz hello tooopen.

    ![Strefa DNS](./media/dns-getstarted-portal/openzone650.png)

4. Na powitania **strefy DNS Utwórz** bloku wprowadź hello następujące wartości, a następnie kliknij przycisk **Utwórz**:


   | **Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Nazwa**|contoso.com|Nazwa Hello hello strefy DNS|
   |**Subskrypcja**|[Twoja subskrypcja]|Wybierz strefę DNS subskrypcji toocreate hello w.|
   |**Grupa zasobów**|**Utwórz nową:** contosoDNSRG|Utwórz grupę zasobów. Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych. więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artykuł z omówieniem.|
   |**Lokalizacja**|Zachodnie stany USA||

> [!NOTE]
> Grupa zasobów Hello odwołuje się lokalizacji toohello hello grupy zasobów, a nie ma wpływu na powitania strefy DNS. Lokalizacja strefy DNS Hello jest zawsze "globalne" i nie jest wyświetlany.

## <a name="create-a-dns-record"></a>Tworzenie rekordu DNS

Witaj poniższy przykład przeprowadzi Cię przez proces hello Tworzenie nowego rekordu "". Inne typy rekordów i istniejące rekordy toomodify, zobacz [rekordy DNS, zarządzanie i zestawów rekordów przy użyciu portalu Azure hello](dns-operations-recordsets-portal.md). 

1. Z hello strefy DNS utworzone w portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**. Kliknij przycisk hello **contoso.com** strefy DNS w hello wszystkich bloku zasobów. Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **contoso.com** w hello **filtrować według nazwy...** pole tooeasily dostępu hello strefy DNS.

1. U góry hello hello **strefy DNS** bloku, wybierz opcję **+ zestawu rekordów** tooopen hello **dodać zestaw rekordów** bloku.

1. Na powitania **dodać zestaw rekordów** bloku, wprowadź następujące wartości hello, a następnie kliknij przycisk **OK**. W tym przykładzie jest tworzony rekord A.

   |**Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Nazwa**|www|Nazwa rekordu hello|
   |**Typ**|A| Typ elementu toocreate rekordów DNS, dopuszczalne wartości to A, AAAA, CNAME, MX, NS, SRV, TXT i PTR.  Aby uzyskać więcej informacji na temat typów rekordów, odwiedź stronę [Omówienie stref i rekordów DNS](dns-zones-records.md).|
   |**Czas wygaśnięcia**|1|Time-to-live hello DNS żądania.|
   |**Jednostka czasu wygaśnięcia**|Godziny|Pomiar wartości czasu wygaśnięcia.|
   |**Adres IP**|ipAddressValue| Ta wartość jest hello adres IP, który jest rozpoznawany jako rekord DNS hello.|

## <a name="view-records"></a>Wyświetlanie rekordów

Hello dolnej części bloku strefy DNS hello zawiera rekordy hello hello strefy DNS. Powinna zostać wyświetlona hello domyślne serwery DNS i SOA rekordy, które są tworzone w każdej strefie, oraz nowych rekordów, które zostały utworzone.

![strefa](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>Aktualizowanie serwerów nazw

Gdy użytkownik stwierdzi, że Twoje strefy DNS i rekordy są skonfigurowane poprawnie należy tooconfigure domenę toouse hello Azure DNS nazwy serwerów nazw. Dzięki temu innym użytkownikom w hello Internet toofind rekordów DNS.

Witaj serwerów nazw dla strefy są podane w hello portalu Azure:

![strefa](./media/dns-getstarted-portal/viewzonens500.png)

Te serwery nazw powinien mieć skonfigurowaną rejestratora nazw domen hello (którego go zakupiono hello nazwa domeny). Rejestratora oferuje tooset opcji hello hello serwery nazw dla domeny hello. Aby uzyskać więcej informacji, zobacz [delegować tooAzure Twojego domeny DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Usuwanie wszystkich zasobów

toodelete wszystkie zasoby są tworzone w tym artykule pełną hello następujące kroki:

1. W portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**. Kliknij przycisk hello **MyResourceGroup** grupa zasobów w hello wszystkich bloku zasobów. Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **MyResourceGroup** w hello **filtrować według nazwy...** Grupa zasobów pole tooeasily dostępu hello.
1. W hello **MyResourceGroup** bloku, kliknij przycisk hello **usunąć** przycisku.
1. Witaj portal wymaga nazwy hello tootype tooconfirm grupy zasobów hello, które mają toodelete go. Kliknij przycisk **usunąć**, typ *MyResourceGroup* hello Nazwa grupy zasobów, klikając **usunąć**. Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów w grupie zasobów hello, więc zawsze tooconfirm się, że zawartość hello grupy zasobów przed jego usunięciem. Hello portal usuwa wszystkie zasoby zawarte w grupie zasobów hello, a następnie usuwa samej grupy zasobów hello. Ten proces trwa kilka minut.


## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat usługi Azure DNS, zobacz [Omówienie usługi Azure DNS](dns-overview.md).

toolearn więcej informacji o zarządzaniu rekordy DNS w usłudze Azure DNS, zobacz [rekordy DNS, zarządzanie i zestawów rekordów przy użyciu portalu Azure hello](dns-operations-recordsets-portal.md).

