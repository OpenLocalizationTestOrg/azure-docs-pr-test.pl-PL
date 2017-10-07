---
title: "Obsługa zapory DB rozwiązania Cosmos aaaAzure & IP kontrola dostępu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zasady kontroli dostępu IP toouse zapory obsługują na kontach bazy danych Azure DB rozwiązania Cosmos."
keywords: "Kontrola dostępu do adresu IP, obsługi zapory"
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: b5cdbdb28e9d7ee0fd0ea54aad277167b699929f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-firewall-support"></a>Obsługa zapory w usłudze Azure DB rozwiązania Cosmos
toosecure dane przechowywane na koncie Azure DB rozwiązania Cosmos bazy danych, rozwiązania Cosmos Azure DB udostępnił pomocy technicznej dla hasła, na podstawie [modelu autoryzacji](https://msdn.microsoft.com/library/azure/dn783368.aspx) , która zawiera kod uwierzytelniania wiadomości Hash-based silne (HMAC). Teraz ponadto klucz tajny toohello na podstawie modelu autoryzacji, bazy danych rozwiązania Cosmos Azure obsługuje zasady na kontroli dostępu na podstawie adresu IP dla strony Obsługa zapory dla ruchu przychodzącego. Ten model jest bardzo podobne reguły zapory toohello systemu tradycyjne bazy danych i zapewnia dodatkowy poziom zabezpieczeń toohello konto bazy danych Azure DB rozwiązania Cosmos. Z tym modelem można skonfigurować dostępne tylko z zatwierdzonych zbiór maszyny toobe konta bazy danych DB rozwiązania Cosmos Azure lub usługi w chmurze. Dostęp tooAzure DB rozwiązania Cosmos zasoby z tych zestawów zatwierdzonych komputery i usługi wymagają nadal hello wywołującego toopresent token prawidłowego autoryzacji.

## <a name="ip-access-control-overview"></a>Omówienie kontroli dostępu dla adresu IP
Domyślnie konto bazy danych Azure DB rozwiązania Cosmos jest dostępny z publicznej sieci internet, tak długo, jak długo Żądanie hello towarzyszy token prawidłowego autoryzacji. Kontrola dostępu oparta na zasadach IP tooconfigure hello użytkownik musi podać hello zbiór adresów IP i zakresów adresów IP w toobe formularza CIDR uwzględnione jako hello białej listy adresów IP klienta, konto bazy danych. Po zastosowaniu tej konfiguracji wszystkich żądań wysyłanych z komputerów spoza tej listy dozwolonych jest blokowana przez serwer hello.  połączenie Hello przetwarzania przepływu dla hello kontroli dostępu na podstawie adresu IP jest opisana w powitania po diagramu.

![Diagram przedstawiający proces łączenia hello kontroli dostępu na podstawie adresu IP](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a>Połączenia z usługi w chmurze
Na platformie Azure usługi w chmurze są bardzo typowy sposób do hostowania warstwy środkowej logiki usługi przy użyciu bazy danych Azure rozwiązania Cosmos. tooenable tooan dostępu do bazy danych Azure rozwiązania Cosmos konto bazy danych z usługi w chmurze, hello publicznego adresu IP usługi w chmurze hello musi być dodany toohello dozwolona lista adresów IP skojarzonych z Twoim kontem bazy danych Azure DB rozwiązania Cosmos przez [Konfigurowanie Witaj zasad kontroli dostępu IP](#configure-ip-policy).  To sprawia, że wszystkie wystąpienia roli usługi w chmurze mogą tooyour dostępu do bazy danych Azure rozwiązania Cosmos konta bazy danych. Można pobrać adresów IP dla usług w chmurze w hello portalu Azure, jak pokazano w powitania po zrzut ekranu.

![Zrzut ekranu przedstawiający hello publicznego adresu IP wyświetlane w portalu Azure hello usługi w chmurze](./media/firewall-support/public-ip-addresses.png)

Skalowanie usługi w chmurze, dodając rolę dodatkowe wystąpienia tych nowych wystąpień automatycznie ma konto bazy danych Azure DB rozwiązania Cosmos toohello dostępu, ponieważ są one częścią hello sama usługa w chmurze.

## <a name="connections-from-virtual-machines"></a>Połączenia z maszyn wirtualnych
[Maszyny wirtualne](https://azure.microsoft.com/services/virtual-machines/) lub [zestawy skalowania maszyny wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) mogą być również używane toohost usług warstwy środkowej przy użyciu bazy danych Azure rozwiązania Cosmos.  tooconfigure hello Azure DB rozwiązania Cosmos bazy danych konta tooallow dostęp z maszyn wirtualnych, publicznych adresów IP maszyny wirtualnej i/lub zestaw skali maszyny wirtualnej musi być skonfigurowany jako jeden hello dozwolone adresy IP dla konta bazy danych Azure DB rozwiązania Cosmos przez [Konfigurowanie zasad kontroli dostępu IP hello](#configure-ip-policy). Można pobrać adresów IP dla maszyn wirtualnych w hello portalu Azure, jak pokazano w powitania po zrzut ekranu.

![Zrzut ekranu przedstawiający publicznego adresu IP dla maszyny wirtualnej, wyświetlane w portalu Azure hello](./media/firewall-support/public-ip-addresses-dns.png)

Podczas dodawania grupy toohello wystąpień dodatkowe maszyny wirtualnej, są automatycznie udostępniane konto bazy danych Azure DB rozwiązania Cosmos tooyour dostępu.

## <a name="connections-from-hello-internet"></a>Połączenia z hello internet
Podczas dostępu bazy danych Azure rozwiązania Cosmos bazy danych konta z komputera na hello internet, hello adres IP klienta lub zakresu adresów IP maszyny hello musi być dodany toohello białej listy adresów IP do hello Azure DB rozwiązania Cosmos konta bazy danych. 

## <a id="configure-ip-policy"></a>Konfigurowanie zasad kontroli dostępu IP hello
zasady kontroli dostępu IP Hello można ustawić w hello portalu Azure lub programistycznie za pomocą [interfejsu wiersza polecenia Azure](cli-samples.md), [programu Azure Powershell](powershell-samples.md), lub hello [interfejsu API REST](/rest/api/documentdb/) aktualizując hello `ipRangeFilter` właściwości. Zakresy adresów IP musi być przecinkami oddzielone i nie może zawierać spacji. Przykład: "13.91.6.132,13.91.6.1/24". Podczas aktualizowania konta bazy danych za pomocą tych metod, można toopopulate się, że wszystkie tooprevent właściwości hello zresetowanie ustawień toodefault.

> [!NOTE]
> Przez włączenie IP zasady kontroli dostępu dla konta bazy danych Azure rozwiązania Cosmos bazy danych, wszystkie tooyour dostępu do bazy danych Azure rozwiązania Cosmos konto bazy danych z komputerów poza hello skonfigurowane dozwolone listę zakresów adresów IP są zablokowane. Z tym modelem przeglądanie hello operacji płaszczyzna danych z portalu hello będzie również integralności hello zablokowanych tooensure kontroli dostępu.

Programowanie toosimplify hello portalu Azure ułatwia Identyfikuj i Dodaj adres IP hello toohello komputera klienta, z białej listy, dzięki czemu aplikacje działające na tym komputerze dostęp hello konta bazy danych Azure rozwiązania Cosmos. Należy pamiętać, wykryto tutaj adres IP klienta hello widziany przez hello portal. Może być powitania klienta adres IP komputera, ale może być również hello adres IP bramy sieci. Nie zapomnij tooremove zanim będzie tooproduction.

tooset hello IP zasad kontroli dostępu w hello portalu Azure, przejdź do bloku konta usługi Azure DB rozwiązania Cosmos toohello, kliknij przycisk **zapory** w menu nawigacji hello, następnie kliknij przycisk **ON** 

![Zrzut ekranu pokazujący sposób tooopen hello bloku zapory w hello portalu Azure](./media/firewall-support/azure-portal-firewall.png)

W okienku nowe hello, określ, czy hello portalu Azure może uzyskać dostęp do konta hello i dodać inne adresów i zakresów zależnie od potrzeb, a następnie kliknij **zapisać**.  

> [!NOTE]
> Po włączeniu zasady kontroli dostępu IP należy adres IP hello tooadd dla hello dostępu toomaintain portalu Azure. Witaj portalu adresy IP są:
> |Region|Adres IP|
> |------|----------|
> |Wszystkie regiony, z wyjątkiem tych określonych poniżej| 104.42.195.92|
> |Niemcy|51.4.229.218|
> |Chiny|139.217.8.252|
> |Administracja USA — Arizona|52.244.48.71|
>

![Zrzut ekranu pokazujący sposób tooconfigure ustawień zapory w hello portalu Azure](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-hello-ip-access-control-policy"></a>Rozwiązywanie problemów z zasad kontroli dostępu IP hello
### <a name="portal-operations"></a>Operacje portalu
Przez włączenie IP zasady kontroli dostępu dla konta bazy danych Azure rozwiązania Cosmos bazy danych, wszystkie tooyour dostępu do bazy danych Azure rozwiązania Cosmos konto bazy danych z komputerów poza hello skonfigurowane dozwolone listę zakresów adresów IP są zablokowane. W związku z tym jeśli chcesz tooenable danych portalu płaszczyzny operacje takie jak przeglądanie kolekcje i kwerendy dokumentów, potrzebujesz tooexplicitly dostęp do usługi Azure portalu przy użyciu hello **zapory** bloku w portalu hello. 

![Zrzut ekranu pokazujący sposób tooenable toohello dostęp do portalu Azure](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a>Zestaw SDK & Rest API
Dla zabezpieczeń ze względu na dostęp za pomocą zestawu SDK lub interfejsu API REST z komputerów nie na powitania listy dozwolonych zwróci ogólnego 404 odpowiedzi nie znaleziono z nie dodatkowych szczegółów. Sprawdź, czy dozwolony hello IP liście skonfigurowane dla konfiguracji prawidłowe zasady hello tooensure konta bazy danych Azure rozwiązania Cosmos bazy danych jest zastosowane tooyour konto bazy danych Azure DB rozwiązania Cosmos.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać informacje o sieci Zobacz wskazówki dotyczące wydajności związanych z [porady dotyczące wydajności](performance-tips.md).

