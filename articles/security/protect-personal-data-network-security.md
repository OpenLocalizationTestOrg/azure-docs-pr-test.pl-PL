---
title: "funkcje zabezpieczeń sieci aaaProtect dane osobowe z platformy Azure | Dokumentacja firmy Microsoft"
description: "Ochrona danych osobowych przy użyciu funkcji zabezpieczeń sieci platformy Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a>Ochrona danych osobowych z funkcjami zabezpieczeń sieci: Brama aplikacji w usłudze Azure i grup zabezpieczeń sieci

Ten artykuł zawiera informacje i procedury, które pomogą Ci użyć danych osobowych tooprotect brama aplikacji w usłudze Azure i grup zabezpieczeń sieci.

Ważnym elementem wielowarstwowy zabezpieczeń strategii tooprotect hello zasad ochrony prywatności danych osobowych jest ochrona przed wspólnej luki w zabezpieczeniach luki w zabezpieczeniach takich jak iniekcja kodu SQL lub skryptów między witrynami. Utrzymywanie ruchu sieciowego niechciane spoza sieci wirtualnej platformy Azure pomaga w ochronie przed potencjalne naruszenie zabezpieczeń danych poufnych i Microsoft Azure oferuje narzędzia toohelp ochronę danych przed atakami.

## <a name="scenario"></a>Scenariusz

Firma rejs dużych, siedzibą w Stanach Zjednoczonych hello, rozwija trasy toooffer jego operacji w Śródziemnego hello, Adriatyku i Bałtyckiego mórz, jak również hello brytyjskich. Do realizacji tych działań, uzyskała kilka mniejszych wycieczkowe wierszy na podstawie w Włochy i Niemczech, Dania hello Zjednoczone Królestwo

Witaj firmie Microsoft Azure toostore danych firmowych w hello w chmurze i uruchamianie aplikacji na maszynach wirtualnych, które przetwarzają i dostęp do tych danych. Te dane obejmują dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej z jej klientów globalnych. Zawiera także tradycyjnych informacje kadr, takie jak adresy, numery telefonów, numery identyfikacyjne podatku i medyczne informacje dotyczące pracowników firmy we wszystkich lokalizacjach. wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność zawierający dane osobowe tootrack relacje z bieżących i starszych klientów.

Pracownikom firmy dostępu hello sieci w biurach zdalnych i podróży agentów znajduje się wokół hello world hello firmy mają dostęp do zasobów firmowych toosome i korzystają z aplikacji sieci web hostowanych w maszynach wirtualnych platformy Azure toointeract z nim.

## <a name="problem-statement"></a>Opis problemu

Hello firmy muszą chronić prywatność hello klientów i pracowników dane osobowe przed atakami, którzy wykorzystać oprogramowanie luk w zabezpieczeniach toorun złośliwy kod, który może ujawniać dane osobowe przechowywane lub używane przez aplikacje oparte na chmurze hello firmy.

## <a name="company-goal"></a>Celem firmy

Hello tooensure celem firmy, który nieautoryzowane osoby nie dostępu do firmowej sieci wirtualnej platformy Azure i hello aplikacji i danych, które znajdują się przez wykorzystywanie znanych luk. 

## <a name="solutions"></a>Rozwiązania

Microsoft Azure oferuje zabezpieczenia toohelp mechanizmów uniemożliwić niepożądanego ruchu wprowadzanie sieciach wirtualnych platformy Azure. Kontrola ruchu przychodzącego i wychodzącego tradycyjnie jest wykonywane przez zapory. Na platformie Azure można użyć hello bramy aplikacji z hello zapory aplikacji sieci Web i grup zabezpieczeń sieci (NSG), które działają jako proste rozproszonej zapory. Te narzędzia umożliwiają toodetect i zablokowanie ruchu sieciowego niepożądane.

### <a name="application-gatewayweb-application-firewall"></a>Aplikacja bramy/Zapora aplikacji sieci Web

Witaj [zapory aplikacji sieci Web](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF) składnik hello [brama aplikacji w usłudze Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) chroni aplikacje sieci web, które są coraz bardziej cele złośliwe ataki wykorzystujące wspólnej znane luki w zabezpieczeniach. Scentralizowane zapory aplikacji sieci Web chroni przed atakami z sieci web i upraszcza zarządzanie zabezpieczeniami bez konieczności wprowadzania zmian w aplikacji.

Azure zapory aplikacji sieci Web adresów różnych kategorii ataku, takich jak iniekcja kodu SQL, skryptów krzyżowych, protokołu HTTP naruszeń i anomalie, robotów, przeszukiwarek, skanerów, Omówiliśmy aplikacji, HTTP "odmowa usługi", i inne typowe ataki, takie jak uruchomienie polecenia, HTTP żądania przemytu, dzielenie odpowiedzi HTTP i ataków dołączenie pliku zdalnego. 

Można utworzyć bramy aplikacji z zapory aplikacji sieci Web, lub dodawanie zapory aplikacji sieci Web tooan istniejącą bramę aplikacji. W obu przypadkach brama aplikacji w usłudze Azure wymaga jego własnej podsieci.

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a>Jak utworzyć bramę aplikacji z zapory aplikacji sieci Web? 

toocreate nową bramę aplikacji z zapory aplikacji sieci Web jest włączona, hello następujące:

1. Dziennik w toohello portalu Azure i hello **ulubione** okienku portalu hello, kliknij polecenie **nowy**

2. W hello **nowy** bloku, kliknij przycisk **sieci**.

3. Kliknij przycisk **brama aplikacji w**.

4. Przejdź toohello portalu Azure, **kliknij nowy \> sieci \> Application Gateway.**

   ![Tworzenie bramy aplikacji](media/protect-netsec/app-gateway-01.png)

5. W hello **podstawy** bloku, zostanie wyświetlone, wprowadź wartości hello hello następujące pola: nazw, warstwy (standardowy lub zapory aplikacji sieci Web), rozmiar jednostki SKU (mały, średni lub duży) wystąpień (2 wysokiej dostępności), liczba subskrypcji, grupy zasobów i Lokalizacja.

6. W hello **ustawienia** bloku, który jest wyświetlany w obszarze **sieci wirtualnej**, kliknij przycisk **wybierz sieć wirtualną**. Ten krok, który otwiera wprowadź hello wybierz bloku sieci wirtualnej.

7. Kliknij przycisk **Utwórz nowy** tooopen hello **Utwórz sieć wirtualną** bloku.

8. Wprowadź hello następujące wartości: nazwa, przestrzeń adresów, nazwy podsieci, zakres adresów podsieci. Kliknij przycisk **OK**.

9. Na powitania **ustawienia** bloku w obszarze **konfiguracji IP frontonu**, wybierz typ adresu IP hello.

10. Kliknij przycisk **wybierz publiczny adres IP,** następnie **Utwórz nowe.**

11. Zaakceptuj wartość domyślną hello, a następnie kliknij przycisk **OK.**

12. Na powitania **ustawienia** bloku w obszarze **konfiguracji odbiornika**, wybierz toouse HTTP lub HTTPS, w obszarze **protokołu**. toouse HTTPS, wymagany jest certyfikat.

13. Konfigurowanie ustawień określonych hello zapory aplikacji sieci Web: **zapory stan** (**włączone**) i **trybie zapory** (**zapobiegania**). Jeśli wybierzesz **wykrywania** jako tryb hello ruchu jest tylko rejestrowane.

14. Przejrzyj hello **Podsumowanie** i kliknij przycisk **OK**. Brama aplikacji hello jest teraz w kolejce, a utworzony.

Po utworzeniu bramy aplikacji hello można znaleźć tooit w portalu hello i kontynuować konfigurację bramy aplikacji hello.

![Brama aplikacji w utworzony](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a>Jak dodać istniejącą aplikację tooan zapory aplikacji sieci Web?

tooupdate istniejących aplikacji bramy toosupport zapory aplikacji sieci Web w trybie zapobiegania hello następujące:

1. W portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**.

2. Kliknij przycisk hello istniejącą bramę aplikacji w hello **wszystkie zasoby** bloku. 
>[!NOTE]
Uwaga: Jeśli subskrypcja hello, już ma kilka zasobów, można wprowadzić nazwę hello w hello filtru według nazwy... Witaj strefy DNS pole tooeasily dostępu.
3. Kliknij przycisk **zapory aplikacji sieci Web** i zaktualizuj ustawienia bramy aplikacji hello: **uaktualnienia tooWAF warstwy** (zaznaczone), **zapory stan** (włączone),  **Tryb zapory** (zapobiegania). Należy również tooconfigure hello zestawu reguł, a następnie skonfiguruj wyłączone reguły.

Aby uzyskać szczegółowe informacje na temat toocreate nową bramę aplikacji z zapory aplikacji sieci Web i w jaki sposób tooadd zapory aplikacji sieci Web tooan istniejącej aplikacji bramy, zobacz [Utwórz bramę aplikacji z zapory aplikacji sieci web przy użyciu portalu hello.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)

### <a name="network-security-groups"></a>Grupy zabezpieczeń sieci

A [sieciowej grupy zabezpieczeń](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) zawiera listę reguł zabezpieczeń, które lub odmawiają tooresources ruchu sieciowego połączone za[sieci wirtualnych Azure](https://docs.microsoft.com/azure/virtual-network/) (VNet). Grupy NSG mogą być skojarzone toosubnets lub poszczególnych maszyn wirtualnych. Gdy grupa NSG jest skojarzona tooa podsieci, mają zastosowanie reguły hello tooall zasobów połączonych toohello podsieci. Dodatkowo można ograniczyć ruch również skojarzyć tooa NSG maszyny Wirtualnej lub karty sieciowej.

Grupy NSG zawierają czterech właściwości: nazwa, Region, grupy zasobów i zasady.
>[!Note]
Mimo że grupy NSG istnieje w grupie zasobów, może być skojarzony tooresources w dowolnej grupie zasobów, tak długo, jak hello zasób jest częścią hello tego samego regionu Azure hello NSG.

Reguły NSG obejmują dziewięć właściwości: nazwa, protokół (TCP, UDP lub \*, w tym protokołu ICMP, a także protokołów UDP i TCP), zakres portów, zakres portów docelowych źródła, adres źródłowy prefiksu, prefiks adresu docelowego, kierunek (przychodzący lub wychodzący) (priorytet od 100 do 4096) oraz dostęp typu (zezwalania lub odmowy). Wszystkie grupy NSG zawierają zestaw reguł domyślnych, które mogą być usunięte lub zastąpione przez utworzone reguły hello.

#### <a name="how-do-i-implement-nsgs"></a>Jak wdrożyć grup NSG?

Wdrażanie grup NSG wymaga planowania i należy tootake pod uwagę kilka zagadnienia dotyczące projektowania. Obejmują one limity hello liczby grup NSG dla każdej subskrypcji i reguł na grupę NSG; Projekt sieci wirtualnej i podsieci, reguły specjalne, ruch protokołu ICMP, izolacji warstwy z podsieci i moduły równoważenia obciążenia.

Aby uzyskać więcej pomocy w planowanie i wdrażanie grup NSG, a przykładowy scenariusz wdrażania, zobacz [filtrowania ruchu sieciowego z grup zabezpieczeń sieci.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)

#### <a name="how-do-i-create-rules-in-an-nsg"></a>Jak utworzyć zasady w grupie NSG?

toocreate reguły w istniejącej grupy NSG dla ruchu przychodzącego, hello następujące:

1. Kliknij przycisk **Przeglądaj**, a następnie **sieciowej grupy zabezpieczeń**.

2. Na liście hello grup NSG, kliknij **frontonu NSG**, a następnie **reguły zabezpieczeń dla ruchu przychodzącego.**

3. Na liście hello reguły zabezpieczeń ruchu przychodzącego, kliknij **Dodaj.**

4. Wprowadź wartości hello hello kolejnych pól: nazwa, priorytet, źródło, protokół, źródła należeć do zakresu, miejsce docelowe docelowy zakres portów i akcji.

Nowa reguła Hello będą wyświetlane w hello NSG po kilku sekundach.

![reguły zabezpieczeń sieci](media/protect-netsec/inbound-security.png)

Aby uzyskać więcej instrukcji dotyczących sposobu toocreate grup NSG w podsieci, utwórz reguły i skojarzeniu grupy NSG z podsiecią frontonu i zaplecza, zobacz [tworzenie grup zabezpieczeń sieci przy użyciu hello portalu Azure.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)

## <a name="next-steps"></a>Następne kroki

[Zabezpieczenia sieci platformy Azure](https://azure.microsoft.com/blog/azure-network-security/)

[Najlepsze rozwiązania sieci platformy Azure](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[Uzyskaj informacje na temat grupy zabezpieczeń sieci](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[Zapora aplikacji sieci Web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
