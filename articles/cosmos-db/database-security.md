---
title: "zabezpieczenia aaaDatabase — bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak bazy danych Azure rozwiązania Cosmos zapewnia ochronę i danych zabezpieczeń bazy danych dla danych."
keywords: "bazy danych nosql, zabezpieczeń, ochrony informacji, bezpieczeństwo danych, szyfrowania bazy danych, ochrona bazy danych, zasady zabezpieczeń testowania zabezpieczeń"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Zabezpieczenia bazy danych w usłudze Azure DB rozwiązania Cosmos

W tym artykule omówiono najlepszych rozwiązań dotyczących zabezpieczeń bazy danych i najważniejsze funkcje oferowane przez toohelp bazy danych Azure rozwiązania Cosmos, zapobiegania, wykrywania i odpowiadać toodatabase naruszeń.
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>What's new in Azure DB rozwiązania Cosmos zabezpieczeń?

Szyfrowanie magazynowanych jest teraz dostępna dla dokumentów i kopie zapasowe przechowywane w usłudze Azure DB rozwiązania Cosmos we wszystkich regionach platformy Azure. Szyfrowanie magazynowanych jest automatycznie stosowane do istniejących i nowych klientów z tych obszarów. Brak tooconfigure nie potrzeba żadnych czynności; Możesz uzyskać tekst hello tego samego opóźnienia doskonały, przepływności, dostępności i funkcji przed z korzyści hello otrzymuje żadnej informacji o danych jest bezpieczne i bezpieczne z szyfrowaniem przechowywane.

## <a name="how-do-i-secure-my-database"></a>Jak zabezpieczyć bazy danych? 

Bezpieczeństwo danych jest udostępniony odpowiedzialność między, powitania klienta i dostawcy bazy danych. W zależności od dostawcy bazy danych hello wybrane hello ilość odpowiedzialność wykonać może się różnić. Jeśli wybierzesz rozwiązania lokalnego, należy tooprovide od zabezpieczeń toophysical ochrony punktu końcowego sprzętu — czyli bez łatwe zadania. Decydując PaaS dostawcy bazy danych w chmurze takich jak bazy danych Azure rozwiązania Cosmos znacznie zmniejsza obszaru zainteresowania. Witaj następujących obrazu, pobierają z firmy Microsoft [obowiązki udostępnionych chmury obliczeniowej](https://aka.ms/sharedresponsibility) oficjalny dokument przedstawia, jak Twoje odpowiedzialność zmniejsza się z dostawcą PaaS, takie jak bazy danych Azure rozwiązania Cosmos.

![Obowiązki klienta i bazy danych dostawcy:](./media/database-security/nosql-database-security-responsibilities.png)

Witaj poprzedniego diagram przedstawia chmury wysokiego poziomu zabezpieczeń składników, ale elementy potrzebujesz tooworry o specjalnie dla własnego rozwiązania bazy danych? I jak porównać tooeach rozwiązań innych? 

Firma Microsoft zaleca powitania po Lista kontrolna wymagań toocompare systemów bazy danych:

- Zabezpieczenia sieci i ustawieniami zapory
- Uwierzytelnianie użytkownika i kontrolek użytkownika szczegółowe
- Możliwość tooreplicate dane globalnie regionalnymi awariami
- Możliwość tooperform przechodzenia w tryb failover z jednym centrum tooanother
- Replikacja danych lokalnych w obrębie centrum danych
- Automatyczne kopie zapasowe
- Przywrócenie usuniętych danych z kopii zapasowych
- Ochrona i izolowanie danych poufnych
- Monitorowanie ataków
- Odpowiada tooattacks
- Możliwość toogeo ogranicznika danych tooadhere toodata ładu ograniczenia
- Fizyczna ochrona serwerach w centrach danych chronionych

I chociaż wydaje się to oczywistym, ostatnie [naruszeń bazy danych na dużą skalę](http://thehackernews.com/2017/01/mongodb-database-security.html) Przypomnij nam hello prostą, ale krytyczne znaczenie hello następujące wymagania:
- Poprawioną serwerów, które są zachowane w górę toodate
- HTTPS przez szyfrowanie domyślne/SSL
- Konta z uprawnieniami administracyjnymi o silnych haseł

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>Jak bazy danych Azure rozwiązania Cosmos zabezpieczyć bazy danych?

Przyjrzyjmy się wstecz hello powyższej listy — jak wiele z tych wymagań zabezpieczeń bazy danych rozwiązania Cosmos Azure zapewnia? Każdy jedno.

Umożliwia pracę na każdej z nich szczegółowo.

|Wymaganie dotyczące zabezpieczeń|Metoda zabezpieczeń Azure DB rozwiązania Cosmos|
|---|---|---|
|Bezpieczeństwo sieci|Za pomocą zapory IP jest hello pierwszą warstwę ochrony toosecure bazy danych. Azure DB rozwiązania Cosmos obsługuje zasady na kontroli dostępu na podstawie adresu IP dla strony Obsługa zapory dla ruchu przychodzącego. Hello kontroli dostępu na podstawie adresu IP są podobne reguły zapory toohello używane przez systemy tradycyjne bazy danych, ale są one rozszerzane tak, aby konto bazy danych Azure DB rozwiązania Cosmos jest dostępna tylko w zatwierdzonym zbiór maszyny lub usługi w chmurze. <br><br>Azure DB rozwiązania Cosmos umożliwia tooenable możesz określonego adresu IP (168.61.48.0), zakresu adresów IP (168.61.48.0/8) i kombinacje adresów IP i zakresów. <br><br>Wszystkie żądania pochodzące z komputerów spoza tej listy dozwolonych są blokowane przez bazy danych Azure rozwiązania Cosmos. Żądania zatwierdzenia maszyn i usługi w chmurze musi wykonaniu toobe proces uwierzytelniania hello podane zasobów toohello kontroli dostępu.<br><br>Dowiedz się więcej w [Obsługa zapory bazy danych Azure rozwiązania Cosmos](firewall-support.md).|
|Autoryzacja|Azure DB rozwiązania Cosmos używa kod uwierzytelniania wiadomości oparty na skrótu (HMAC) do autoryzacji. <br><br>Każde żądanie jest generowany skrót przy użyciu klucza tajnego konta hello i hello kolejnych base-64 zakodowanego wyznaczania wartości skrótu są wysyłane z każdego wywołania tooAzure DB rozwiązania Cosmos. Witaj toovalidate żądanie używa usługi Azure DB rozwiązania Cosmos hello hello poprawny klucz tajny i właściwości toogenerate skrót, a następnie porównuje wartości hello z jedną hello w żądaniu hello. Jeśli Witaj dwie wartości są takie same, operacja hello jest autoryzowany pomyślnie i hello żądanie jest przetwarzane, w przeciwnym razie braku autoryzacji i hello żądanie zostało odrzucone.<br><br>Możesz użyć dowolnej [klucza głównego](secure-access-to-data.md#master-keys), lub [token zasobu](secure-access-to-data.md#resource-tokens) umożliwiające dostęp do szczegółowych tooa zasobów takich jak dokumentu.<br><br>Dowiedz się więcej w [zabezpieczanie dostępu do zasobów DB rozwiązania Cosmos tooAzure](secure-access-to-data.md).|
|Uprawnienia użytkowników i|Przy użyciu hello [klucza głównego](#master-key) hello konta, można utworzyć zasobów użytkowników i uprawnienia dla jednej bazy danych. A [token zasobu](#resource-token) jest skojarzony z uprawnień w bazie danych i określa, czy hello użytkownik ma dostęp (odczytu i zapisu, tylko do odczytu, lub Brak dostępu) zasobu usługi application tooan hello bazy danych. Zasoby aplikacji obejmują kolekcje, dokumenty, załączniki, procedur składowanych, wyzwalaczy i funkcji UDF. token zasobu Hello jest, a następnie używane podczas uwierzytelniania tooprovide lub odmówić dostępu toohello zasobów.<br><br>Dowiedz się więcej w [zabezpieczanie dostępu do zasobów DB rozwiązania Cosmos tooAzure](secure-access-to-data.md).|
|Integracja usługi Active directory (RBAC)| Można też podać konto bazy danych toohello dostępu za pomocą kontroli dostępu (IAM) w hello portalu Azure, jak pokazano na zrzucie ekranu pokazano hello, poniżej tej tabeli. IAM umożliwia kontroli dostępu opartej na rolach i integruje się z usługą Active Directory. Role wbudowane lub role niestandardowe można użyć dla użytkowników indywidualnych i grup, jak pokazano w powitania po obrazu.|
|Globalne replikacji|Azure DB rozwiązania Cosmos oferuje gotowe dystrybucji globalny, co pozwala tooreplicate Twojego tooany danych, kliknij jeden z centrów danych na całym świecie platformy Azure z hello przycisku. Globalne replikacji umożliwia globalne skalowanie i podaj dane tooyour małych opóźnieniach dostępu wokół hello world.<br><br>W kontekście hello zabezpieczeń globalnych replikacji temu ochronę danych przed regionalnymi awariami.<br><br>Dowiedz się więcej w [globalnie dystrybucji danych](distribute-data-globally.md).|
|Regionalnej pracy w trybie Failover|Jeśli zostały zreplikowane dane w więcej niż jednego centrum danych, bazy danych rozwiązania Cosmos Azure automatycznie najedzie na operacje powinny centrum danych regionalnych przejścia do trybu offline. Można utworzyć listę regionów trybu failover przy użyciu hello regionów, w których dane są replikowane z określonymi priorytetami. <br><br>Dowiedz się więcej w [regionalnej pracy w trybie Failover w usłudze Azure DB rozwiązania Cosmos](regional-failover.md).|
|Lokalnej replikacji|Nawet w ramach jednego centrum danych, bazy danych rozwiązania Cosmos Azure automatycznie replikuje dane dotyczące wysokiej dostępności nadanie hello wybór [poziomy spójności](consistency-levels.md). Gwarantuje to [dostępność czas działania 99,99%](https://azure.microsoft.com/support/legal/sla/cosmos-db) i pochodzi z gwarancją finansowych - coś zapewniają żadnej innej usługi bazy danych.|
|Automatyczne kopie zapasowe online|Azure DB rozwiązania Cosmos baz danych są regularnie wykonywana kopia zapasowa i przechowywane w magazynie georedundant. <br><br>Dowiedz się więcej w [automatyczne kopie zapasowe online i przywracania bazy danych Azure rozwiązania Cosmos](online-backup-and-restore.md).|
|Przywracanie usuniętych danych|Hello automatycznych kopii zapasowych online może być używane toorecover danych mogą przypadkowo usunięto się zbyt ~ 30 dni po zdarzeniu hello. <br><br>Dowiedz się więcej [automatyczne kopie zapasowe online i przywracania bazy danych Azure rozwiązania Cosmos](online-backup-and-restore.md)|
|Ochrona i izolowanie danych poufnych|Wszystkie dane w regionach hello na liście [nowości?](#whats-new) teraz jest szyfrowane, gdy.<br><br>Dane osobowe i innych poufnych danych mogą być izolowane toospecific kolekcje i odczytu i zapisu lub dostęp tylko do odczytu mogą być ograniczone toospecific użytkowników.|
|Monitor łącznego czasu ataków|Przy użyciu rejestrowania inspekcji i Dzienniki aktywności, można monitorować konto dla typowych i nietypowych działań. Można wyświetlić, jakie operacje były wykonywane na zasoby, które zainicjować operacji hello, w przypadku operacji hello Wystąpił stan hello hello operacji i bardziej, jak pokazano na powitania zrzut ekranu poniżej tej tabeli.|
|Odpowiedź tooattacks|Gdy nawiązano tooreport pomocy technicznej platformy Azure potencjalny atak proces odpowiedzi na zdarzenia krok 5 zostało rozpoczęte. Celem Hello hello kroku 5 procesu jest toorestore normalnej pracy zabezpieczenia i operacje możliwie jak najszybciej po zostanie wykryty problem i dochodzenia została uruchomiona.<br><br>Dowiedz się więcej w [Response zabezpieczeń firmy Microsoft Azure w chmurze hello](https://aka.ms/securityresponsepaper).|
|Grodzenia|Azure DB rozwiązania Cosmos zapewnia zarządzanie danymi i zgodności dla suwerennych regionów (na przykład Niemczech, Chinach, nam wersji dla instytucji rządowych).|
|Urządzenia chronione|Dane w usłudze Azure DB rozwiązania Cosmos są przechowywane na dyskach SSD w centrach danych chronionych na platformie Azure.<br><br>Dowiedz się więcej [Globalne centra danych firmy Microsoft](https://www.microsoft.com/en-us/cloud-platform/global-datacenters)|
|Szyfrowanie protokołu HTTPS/SSL/TLS|Wszystkie interakcje bazy danych rozwiązania Cosmos Azure Usługa klienta są SSL/TLS 1.2, wymuszane. Ponadto wszystkie replikacji wewnątrz centrum danych i między centrum danych jest SSL/TLS 1.2, wymuszane.|
|Szyfrowanie w spoczynku|Wszystkie dane przechowywane w bazie danych rozwiązania Cosmos Azure jest szyfrowane, gdy. Dowiedz się więcej [szyfrowania bazy danych Azure rozwiązania Cosmos w stanie spoczynku](.\database-encryption-at-rest.md)|
|Poprawioną serwerów|Jako zarządzane bazy danych bazy danych Azure rozwiązania Cosmos eliminuje hello potrzeby toomanage i poprawki serwerów, które jest wykonywane, automatycznie.|
|Konta z uprawnieniami administracyjnymi o silnych haseł|Jego twardych toobelieve który mamy nawet musi toomention to wymaganie, ale w przeciwieństwie do niektórych naszych konkurencji jest niemożliwe toohave konto administracyjne bez hasła w usłudze Azure DB rozwiązania Cosmos.<br><br> Zabezpieczenia za pośrednictwem protokołu SSL i HMAC tajny uwierzytelnianie oparte na jest rozszerzania w domyślnie.|
|Certyfikaty ochrony zabezpieczeń i danych|Zawiera bazę danych systemu Azure rozwiązania Cosmos [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001), [europejskiego modelu klauzule (EUMC)](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses), i [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) certyfikaty. Dodatkowe certyfikaty są w toku.|

Witaj Poniższy zrzut ekranu przedstawia integracji usługi Active directory (RBAC) za pomocą kontroli dostępu (IAM) w portalu Azure hello: ![dostępu do formantu (IAM) w hello portal Azure — prezentacja zabezpieczeń bazy danych](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

Witaj Poniższy zrzut ekranu przedstawia sposób korzystania z rejestrowania inspekcji i działania dzienniki toomonitor Twojego konta: ![działania w dziennikach bazy danych Azure rozwiązania Cosmos](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat kluczy głównych i tokenów zasobów zobacz [tooAzure dostępu Zabezpieczanie danych DB rozwiązania Cosmos](secure-access-to-data.md).

Aby uzyskać więcej informacji o certyfikatach firmy Microsoft, zobacz [Centrum zaufania Azure](https://azure.microsoft.com/support/trust-center/).
