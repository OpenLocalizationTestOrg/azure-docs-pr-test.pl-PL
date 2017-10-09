---
title: "aaaChange hello rozliczenia dotyczące usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toostop są rozliczane usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>Migrowanie z usługi Azure RemoteApp tooMyCloudIT 

**Aktualnie używasz usługi Microsoft Azure RemoteApp?** : MyCloudIT wbudowane toomigrate automatyczne narzędzie Azure RemoteApp (ARA) kolekcji toohello MyCloudIT platformy do zarządzania, pozostawiając toorun w systemie Microsoft Azure.

**Korzystać z portalu usługi Azure Resource Manager hello**: zakończone migracji na platformie MyCloudIT hello umożliwia natychmiastowy dostęp tooAzure nowego portalu usługi Azure Resource Manager. Ten portal zawiera wszystkie nowe możliwości hello i innowacje oferowane przez Microsoft Azure, tym tooensure rozmiary maszyny tooVirtual dostępu wdrożenia jest zbudowany toosupport hello wymagania firmy.

**Testu w równoległych tooensure hello odpowiednie rozwiązanie dla potrzeb**: narzędzie migracji MyCloudIT hello jest wbudowany proces migracji hello tooinitiate i równoległych czasu użytkowników ARA kontynuować toouse ARA testu.  Użytkownicy pozostanie w ARA do migracji i testowania są spełnione.  Narzędzie migracji Hello jest wbudowana toohandle hello typowe ARA kolekcji.  Jeśli uważasz, że masz unikatowy, niestandardowym scenariusz, skontaktuj się z nami pod adresem [ sales@conexlink.com ](mailto:sales@conexlink.com) , firma Microsoft może zapewnić tooassist dopasowane planu migracji.

**Funkcje pulpitu jako usługa**: należy pamiętać, że MyCloudIT nie tylko zapewnia zazwyczaj używany do funkcji Połączenia programów RemoteApp hello, ale oferujemy również pełny pulpit jako A — Usługa możliwości hello sam koszt miesięcznie bez żadnych minimalna użytkownika wymagania.

## <a name="what-we-will-do-for-you"></a>Wykonamy dla Ciebie

MyCloudIT automatyzuje migracji hello szablonu usługi Azure RemoteApp z hello klasycznego portalu Azure z Twojej subskrypcji toohello Portal Azure Resource Manager subskrypcji z naszego narzędzia automatycznej migracji.  

> [!NOTE]
> Hello Azure RemoteApp, szablon musi pozostać w hello tego samego regionu Azure oryginalnego wdrożenia usługi Azure RemoteApp.  Jeśli potrzebujesz podczas migracji hello toochange regiony platformy Azure lub subskrypcji platformy Azure, skontaktuj się z nami Aby uzyskać dodatkowe wskazówki na [ sales@conexlink.com ](mailto:sales@conexlink.com).

Przeczytaj poniższe informacje, aby uzyskać szczegółowe informacje o hello zautomatyzowanego procesu migracji z hello MyCloudIT narzędzia migracji:

1. Narzędzie migracji Hello skanuje subskrypcjach bieżącej dla wszystkich istniejących wdrożeń ARA.  
2. Wybierz jeden toomigrate kolekcji ARA naraz.  Jeśli masz wiele kolekcji, należy uruchomić narzędzie naszym wielokrotnie.
3. Masz hello opcja toocopy hello dyski profilu użytkownika (UPD) tooyour nowe wdrożenie, możesz pobrać starszych danych, lub ręcznie zmapuj UPD toohello nowego wdrożenia. Jeśli wybierzesz toocopy Twojego UPD, możemy zapisać UPD hello i obejmują plik tekstowy, który mapuje nazwę hello UPD nazwa tooeach użytkowników.  Hello UPD zostaną skopiowane tooa udziału na serwerze RDSMGMT hello `F:\Shares\LegacyUPD` i mają być widoczne za pośrednictwem udziału hello `\\RDSmgmt\LegacyUPD`. 
4. Migracja wymaga bieżącego wdrożenia ARA bez przestojów.  Jednak jeśli po kopiowania hello zmian toohello UPD (z ARA), te zmiany nie zostaną odzwierciedlone w UPD hello przechowywane w portalu usługi Azure Resource Manager hello. 
5. Jeśli masz dodatkowe maszyny wirtualne, takie jak kontrolerów domeny i serwerów plików w klasycznej sieci wirtualnej platformy Azure będzie nawiązanie komunikacji równorzędnej między istniejących klasycznego Azure sieci wirtualnej sieci wirtualnej, hello nową sieć wirtualną utworzymy dla Ciebie w hello nowego zasobu platformy Azure Menedżer portalu.
6. Nasze zautomatyzowane rozwiązanie tylko ustanowi wirtualne sieci równorzędne — od istniejących klasycznego Azure sieci wirtualnej i hello nową sieć wirtualną w przypadku istniejącego wdrożenia ARA wdrożenia hybrydowego; to znaczy, są uwierzytelniani z serwera Active Directory kontrolera domeny systemu Windows w hello istniejących klasycznej sieci wirtualnej. Nie możemy ustanowić wirtualne sieci równorzędne — kolekcji, ale wymagają wirtualne sieci równorzędne —, skontaktuj się z nami jako [ sales@conexlink.com ](mailto:sales@conexlink.com) i będzie tooconfigure wszystkiego sieci wirtualnej komunikacji równorzędnej bez ponoszenia dodatkowych kosztów.
7. Nasze zautomatyzowane rozwiązanie zapewnia konfigurację usługi Azure DNS są aktualizowane za pomocą hello nowej sieci wirtualnej ustawienia tooensure nowego wdrożenia można połączyć tooyour istniejącego kontrolera domeny w hello klasycznej sieci wirtualnej.
8. Nasze zautomatyzowane rozwiązanie będzie Sprawdź, czy nie konflikty adresów IP jak możemy utworzyć tej nowej sieci wirtualnej i ustanowienia hello sieci wirtualnej komunikacji równorzędnej dla wdrożenia, których istniejącego serwera systemu Windows Server Active Directory.
9. Jeśli używane są tylko usługi Azure AD do uwierzytelniania, MyCloudIT utworzy nowy domenie systemu Windows Server Active Directory i Azure AD Connect toosynchronize użytkownicy między hello istniejącego wystąpienia usługi Azure AD i hello utworzenia nowego systemu Windows Server domeny usługi Active Directory przez MyCloudIT.
10. Jeśli używasz systemu Windows Server domeny usługi Active Directory tooauthenticate ARA użytkowników naszego zautomatyzowane rozwiązanie będzie łączyć nowego tooyour w wdrożenia MyCloudIT istniejących systemu Windows Server Active Directory kontrolera domeny za pośrednictwem sieci wirtualnej komunikacji równorzędnej.
11. Jeśli używasz usługi Azure Active Directory Domain Services uwierzytelniania został migracji można, ale skontaktuj się z nami, można utworzyć plan niestandardowy migracji dla Ciebie.  Wyślij wiadomość e-mail zbyt[sales@conexlink.com](mailto:sales@conexlink.com). 
12. Po migracji toobe kolekcji hello jest potwierdzone, zaczekaj i zwalnia podczas naszych zautomatyzowane rozwiązanie migruje ARA kolekcji, a nowe rozwiązanie aplikacji zdalnych MyCloudIT zmiennych dyski profilu użytkownika toohello (opcjonalnie).
13. Po zakończeniu wdrażania hello firma Microsoft będzie ponownie opublikować hello tych samych aplikacji, które zostały opublikowane w ARA i po wdrożeniu, będziesz w stanie toopublish dodatkowe aplikacje.

## <a name="post-migration-benefits"></a>Po migracji korzyści

1. Udostępniamy konsoli zarządzania hello umożliwiający toomanage hello pełnego cyklu życia wdrożenia aplikacji zdalnych.
2. Będzie możliwe toomanage sieci wirtualnej maszyny z portalu.  Rozpocznij / Zatrzymaj, a następnie zmień rozmiar poszczególnych maszyn wirtualnych w razie potrzeby.
3. Konsola zarządzania Hello zapewnia hello toocreate możliwości i zarządzanie użytkownikami / grupy z portalu zarządzania.
4. Konsola zarządzania Hello oferuje hello możliwości toosynchronize użytkowników z usługi Office 365 toocreate tego samego środowiska logowania.
5. Witaj Konsola zarządzania zapewnia toocreate możliwości hello dodatkowe RemoteApp i pulpitu kolekcji bez kosztów zduplikowanego użytkownika lub użytkownika minimalne wymagania. 
6. Konsola zarządzania Hello oferuje możliwości hello toopublish nowych aplikacji zdalnych aplikacji.
7. Konsola zarządzania Hello zapewnia hello możliwości tooschedule hello uruchamiania i wyłączania wdrożenia aplikacji zdalnych czy rozwiązania potrzebne tylko w określonych godzinach.
8. Konsola zarządzania Hello oferuje hello możliwości tooautomate hello instalacji i konfiguracji agenta usługi Kopia zapasowa Azure hello, co zapewnia historii przechowywania dokumentów dla danych klienta.
9. Konsola zarządzania Hello zapewnia dostęp do metryk tooperformance wdrożenia.  Dzięki temu hello żadnych wąskich gardeł wydajności tooidentify możliwości bez instalowania narzędzi do zarządzania wyższą wydajność.
10. Jeśli masz wiele hostów sesji będzie automatycznie stanie tooenable skalowanie tak tylko sesji hello hostów, które muszą toobe uruchomione są uruchomione.
11. MyCloudIT udostępnia serwer bramy RDWeb toohello dostęp za pośrednictwem MyCloudIT nazwy domeny.  Firma Microsoft udostępnia również hello możliwości mapy toore hello adresu URL tooa niestandardowy adres URL dla użytkownika końcowego znakowania.

## <a name="prerequisites-for-migration"></a>Wymagania wstępne dotyczące migracji

1. Musi mieć dostęp toohello subskrypcji Azure, która obsługuje bieżącego rozwiązania Azure RemoteApp.
2. Musi udzielić naszego portalu uprawnień w ramach Twojej subskrypcji toomigrate szablonu, a toocreate / modify nowego wdrożenia MyCloudIT.
3. Należy pamiętać, że ze względu na ograniczenia tooa w usłudze Azure RemoteApp, każda kolekcja tylko można przeprowadzić trzy razy.  Należy toomigrate kolekcji więcej niż trzy razy, możesz podnieść tooincrease tooAzure biletu liczba eksportu, lub skontaktuj się z nami i firma Microsoft pomoże hello ARA żądania tooincrease hello eksportu count.

## <a name="mycloudit-billing"></a>MyCloudIT rozliczeń

Można znaleźć pod adresem [MyCloudIT ceny rozwiązań RemoteApp](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) Aby uzyskać informacje na temat toopredict i zarządzanie nimi koszty ogólne Azure.

Jeśli nadal masz pytania, skontaktuj się z nami pod adresem [ sales@conexlink.com ](mailto:sales@conexlink.com) lub Obejrzyj prezentację pełne hello [narzędzie migracji usługi Azure RemoteApp - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

