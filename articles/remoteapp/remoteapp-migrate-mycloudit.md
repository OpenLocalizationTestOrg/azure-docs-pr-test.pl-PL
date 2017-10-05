---
title: "Zmień rozliczenia dotyczące usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zatrzymać są rozliczane usługi Azure RemoteApp."
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
ms.openlocfilehash: 32fc673eeef01e80c73375bf264206beea8cfbe5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="migrate-from-azure-remoteapp-to-mycloudit"></a>Migracja z usługi Azure RemoteApp do MyCloudIT 

**Aktualnie używasz usługi Microsoft Azure RemoteApp?** : MyCloudIT wbudowane automatyczne narzędzie do migracji z kolekcji usługi Azure RemoteApp (ARA) do platformy zarządzania MyCloudIT pracując nadal na Microsoft Azure.

**Korzystanie z portalu usługi Azure Resource Manager**: zakończone migracji na platformie MyCloudIT umożliwia natychmiastowy dostęp do nowego portalu usługi Azure Resource Manager platformy Azure. Ten portal zawiera nowe funkcje i innowacje oferowane przez Microsoft Azure, łącznie z dostępem do rozmiarów maszyn wirtualnych w celu zapewnienia wdrożenia korzysta z wbudowanej obsługi wymagania firmy.

**Test równolegle zapewnić odpowiednie rozwiązanie dla potrzeb**: narzędzie migracji MyCloudIT korzysta z wbudowanej zainicjowania procesu migracji i równoległych czasu użytkowników ARA nadal używać ARA testu.  Użytkownicy pozostanie w ARA do migracji i testowania są spełnione.  Narzędzie do migracji korzysta z wbudowanej obsługi typowych kolekcji ARA.  Jeśli uważasz, że masz unikatowy, niestandardowym scenariusz, skontaktuj się z nami pod adresem [ sales@conexlink.com ](mailto:sales@conexlink.com) , firma Microsoft udostępnia dopasowane planu z migracji.

**Funkcje pulpitu jako usługa**: należy pamiętać, że MyCloudIT nie tylko oferuje możliwości usługi RemoteApp jest przyzwyczajony do, ale oferujemy również pełny pulpit jako A — Usługa możliwości kosztów samej miesięcznie bez żadnych minimalna użytkownika wymagania.

## <a name="what-we-will-do-for-you"></a>Wykonamy dla Ciebie

MyCloudIT automatyzuje migracji szablonu usługi Azure RemoteApp z portalu klasycznego Azure subskrypcji do portalu Azure Resource Manager subskrypcji z naszego narzędzia automatycznej migracji.  

> [!NOTE]
> Szablon usługi Azure RemoteApp muszą pozostać w tym samym regionie Azure jako oryginalnego wdrożenia usługi Azure RemoteApp.  Jeśli potrzebujesz zmienić regiony platformy Azure lub subskrypcji platformy Azure, podczas migracji, skontaktuj się z nami Aby uzyskać dodatkowe wskazówki na [ sales@conexlink.com ](mailto:sales@conexlink.com).

Przeczytaj poniższe informacje, aby uzyskać szczegółowe informacje na temat procesu automatycznej migracji za pomocą narzędzia migracji MyCloudIT:

1. Narzędzie do migracji skanuje subskrypcjach bieżącej dla wszystkich istniejących wdrożeń ARA.  
2. Wybierz jedną kolekcję ARA migracji naraz.  Jeśli masz wiele kolekcji, należy uruchomić narzędzie naszym wielokrotnie.
3. Istnieje możliwość kopiowania dysków profilu użytkownika (UPD) do nowego wdrożenia, możesz pobrać starszych danych, lub ręcznie mapowania sieci UPD nowego wdrożenia. Jeśli chcesz skopiować z UPD możemy zapisać UPD i obejmują plik tekstowy, który mapuje nazwę UPD nazwy poszczególnych użytkowników.  UPD zostaną skopiowane do udziału na serwerze RDSMGMT `F:\Shares\LegacyUPD` i mają być widoczne za pośrednictwem udziału `\\RDSmgmt\LegacyUPD`. 
4. Migracja wymaga bieżącego wdrożenia ARA bez przestojów.  Jednak jeśli zmian do UPD (z ARA) po kopii, te zmiany nie zostaną odzwierciedlone w UPD przechowywane w portalu usługi Azure Resource Manager. 
5. Jeśli masz dodatkowe maszyny wirtualne, takie jak kontrolerów domeny i serwerów plików w klasycznej sieci wirtualnej platformy Azure będzie nawiązanie wirtualne sieci równorzędne — między istniejących klasycznego Azure sieci wirtualnej i nową sieć wirtualną, utworzymy dla Ciebie, nowy zasób platformy Azure Menedżer portalu.
6. Nasze zautomatyzowane rozwiązanie tylko ustanowią sieci równorzędne — między istniejących klasycznego Azure sieci wirtualnej i nową sieć wirtualną w przypadku istniejącego wdrożenia ARA wdrożenia hybrydowego; to znaczy, są uwierzytelniani z systemu Windows Server Active Directory kontrolera domeny w istniejącej sieci wirtualnej klasycznego. Nie możemy ustanowić wirtualne sieci równorzędne — kolekcji, ale wymagają wirtualne sieci równorzędne —, skontaktuj się z nami jako [ sales@conexlink.com ](mailto:sales@conexlink.com) i będzie wszystkiego skonfigurować wirtualne sieci równorzędne — bez ponoszenia dodatkowych kosztów.
7. Nasze zautomatyzowane rozwiązanie zapewni konfigurację usługi Azure DNS zostanie zaktualizowany przy użyciu nowych ustawień sieci wirtualnej, aby upewnić się, że nowe wdrożenia może nawiązać połączenie z istniejącego kontrolera domeny w klasycznej sieci wirtualnej.
8. Nasze zautomatyzowane rozwiązanie będzie Sprawdź, czy nie konflikty adresów IP jak możemy utworzyć tej nowej sieci wirtualnej i ustanowienia sieci wirtualnej komunikacji równorzędnej dla wdrożenia, których istniejącego serwera systemu Windows Server Active Directory.
9. Jeśli używane są tylko usługi Azure AD do uwierzytelniania, MyCloudIT utworzy nowej domenie systemu Windows Server Active Directory i Azure AD Connect umożliwia synchronizowanie użytkowników z istniejącym wystąpieniem usługi Azure AD i nowej domeny systemu Windows Server Active katalogu utworzone przez MyCloudIT.
10. Jeśli używasz systemu Windows Server domeny usługi Active Directory do uwierzytelniania użytkowników ARA, naszych zautomatyzowane rozwiązanie połączy nowego wdrożenia MyCloudIT do istniejącego systemu Windows Server Active Directory kontrolera domeny za pośrednictwem sieci wirtualnej komunikacji równorzędnej.
11. Jeśli używasz usługi Azure Active Directory Domain Services uwierzytelniania został migracji można, ale skontaktuj się z nami, można utworzyć plan niestandardowy migracji dla Ciebie.  Wyślij wiadomość e-mail na adres [ sales@conexlink.com ](mailto:sales@conexlink.com). 
12. Po potwierdzeniu kolekcji do migracji, zaczekaj i zwalnia podczas naszych zautomatyzowane rozwiązanie migruje ARA kolekcji, a dyski profilu użytkownika (opcjonalnie) do nowego MyCloudIT, zmiennych rozwiązania aplikacji zdalnych.
13. Po zakończeniu wdrażania, firma Microsoft ponownie opublikować te same aplikacje, które zostały opublikowane w ARA i po wdrożeniu będzie można opublikować dodatkowe aplikacje.

## <a name="post-migration-benefits"></a>Po migracji korzyści

1. Udostępniamy konsoli zarządzania, który umożliwia zarządzanie pełnego cyklu życia wdrożenia aplikacji zdalnych.
2. Będzie można zarządzać maszyn wirtualnych z portalu.  Rozpocznij / Zatrzymaj, a następnie zmień rozmiar poszczególnych maszyn wirtualnych w razie potrzeby.
3. Konsola zarządzania umożliwia tworzenie i zarządzanie nimi użytkowników / grupy z portalu zarządzania.
4. Konsola zarządzania zapewnia możliwość synchronizowania użytkowników z usługą Office 365, aby utworzyć tego samego środowiska logowania.
5. Konsola zarządzania zapewnia możliwość tworzenia dodatkowych RemoteApp i pulpitu kolekcji bez kosztów zduplikowanego użytkownika lub wymagania minimalne użytkownika. 
6. Konsola zarządzania zapewnia możliwość publikowania nowej aplikacji aplikacji zdalnych.
7. Konsola zarządzania umożliwia zaplanowanie uruchamiania i wyłączania wdrożenia aplikacji zdalnych, czy rozwiązania potrzebne tylko w określonych godzinach.
8. Konsola zarządzania umożliwia automatyzację instalacji i konfiguracji agenta usługi Kopia zapasowa Azure, co zapewnia historii przechowywania dokumentów dla danych klienta.
9. Konsola zarządzania udostępnia metryki wydajności wdrożenia.  Zapewnia możliwość identyfikacji dowolnego wąskich gardeł wydajności bez instalowania narzędzi do zarządzania wyższą wydajność.
10. Jeśli masz wiele hostów sesji, można włączyć automatyczne skalowanie tylko sesji, w której działają hostów, które muszą być uruchomione.
11. MyCloudIT zapewnia dostęp do serwera bramy RDWeb za pośrednictwem MyCloudIT nazwy domeny.  Firma Microsoft udostępnia również możliwość ponownego mapowania adres URL, który niestandardowy adres URL dla użytkownika końcowego znakowania.

## <a name="prerequisites-for-migration"></a>Wymagania wstępne dotyczące migracji

1. Musi mieć dostęp do subskrypcji Azure, która obsługuje bieżącego rozwiązania Azure RemoteApp.
2. W ramach subskrypcji migracji szablonu, a także Utwórz / Modyfikuj nowego wdrożenia MyCloudIT należy przyznać naszego portalu uprawnienia.
3. Należy pamiętać, że z powodu ograniczenia w usłudze Azure RemoteApp, każda kolekcja tylko mogą być migrowane trzy razy.  Jeśli chcesz przeprowadzić migrację kolekcji więcej niż trzy razy, możesz podnieść biletu na platformie Azure, aby zwiększyć liczbę sieci eksportu, lub skontaktuj się z nami i firma Microsoft pomoże w żądaniu ARA, aby zwiększyć liczbę eksportu.

## <a name="mycloudit-billing"></a>MyCloudIT rozliczeń

Można znaleźć pod adresem [MyCloudIT ceny rozwiązań RemoteApp](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) Aby uzyskać informacje dotyczące prognozowania i zarządzanie nimi koszty ogólne Azure.

Jeśli nadal masz pytania, skontaktuj się z nami pod adresem [ sales@conexlink.com ](mailto:sales@conexlink.com) lub Obejrzyj prezentację pełne [narzędzie migracji usługi Azure RemoteApp - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

