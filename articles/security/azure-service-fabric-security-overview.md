---
title: "Omówienie zabezpieczeń sieci szkieletowej usług aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie hello zabezpieczeń sieci szkieletowej usług Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: ec5355983c5d59f4e0c3b855965f03ac47f1a4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-overview"></a>Omówienie zabezpieczeń usługi Azure Service Fabric
[Sieć szkieletowa usług Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) to platforma systemów rozproszonych, dzięki którym toopackage łatwe wdrażanie i zarządzanie nimi skalowalne i niezawodne micro-services. Sieci szkieletowej usług uwzględniają hello istotne problemy w tworzenie i zarządzanie aplikacjami w chmurze. Deweloperzy i administratorzy mogą uniknąć złożonych problemów związanych z infrastrukturą i skoncentrować się na implementowaniu wymagających obciążeń o znaczeniu strategicznym, które są skalowalne, niezawodne i łatwe w zarządzaniu.

W tym artykule Omówienie zabezpieczeń usługi Azure w sieci szkieletowej koncentruje się na powitania w następujących obszarach:

-   Zabezpieczanie klastra
-   Monitorowania i diagnostyki
-   Zabezpieczenia przy użyciu certyfikatów
-   Kontrola dostępu oparta na rolach (RBAC)
-   Zabezpieczanie klastra przy użyciu zabezpieczeń systemu Windows
-   Konfigurowanie zabezpieczeń aplikacji w sieci szkieletowej usług
-   Zabezpieczenia komunikacji dla usługi Azure Service Fabric zabezpieczeń

## <a name="securing-your-cluster"></a>Zabezpieczanie klastra
Azure Service Fabric jest orchestrator usług klastrze maszyn, klastrów muszą być użytkownikami zabezpieczonych tooprevent nieautoryzowany łączenie tooyour klastra, szczególnie w przypadku, gdy ma na nim uruchomione obciążeń produkcyjnych. Możliwe toocreate niezabezpieczona klastra, ale dzięki temu tooit tooconnect użytkowników anonimowych, jeśli eksponuje toohello punkty końcowe zarządzania publicznej sieci Internet.

Ta sekcja zawiera omówienie hello scenariusze zabezpieczeń w przypadku klastrów w systemie Azure albo autonomiczne i hello różne technologie używane tooimplement tych scenariuszy. scenariusze zabezpieczeń klastra Hello są następujące:

-   Zabezpieczenia węzła do węzła
-   Węzeł klienta zabezpieczeń

### <a name="node-to-node-security"></a>Zabezpieczenia węzła do węzła
Zabezpiecza komunikację między hello maszyn wirtualnych lub maszyn w klastrze hello. Daje to pewność, że tylko komputery, które są autoryzowane toojoin hello klastra mogą uczestniczyć w hosting aplikacji i usług w klastrze hello.

Klastry z systemem Azure lub autonomiczne klastry z systemem Windows można użyć dowolnego [certyfikatu zabezpieczeń](https://msdn.microsoft.com/library/ff649801.aspx) lub [zabezpieczenia systemu Windows](https://msdn.microsoft.com/library/ff649396.aspx) dla komputerów z systemem Windows Server.

**Zabezpieczenia certyfikatów węzła do węzła**

Sieć szkieletowa usług korzysta z certyfikatów X.509, określone jako część konfiguracji typu węzła hello podczas tworzenia klastra. Certyfikaty te są to szybki przegląd i [sposób uzyskiwania lub je utworzyć znajduje się w tym artykule](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates).

Certyfikat zabezpieczeń jest skonfigurowany podczas tworzenia klastra hello za pośrednictwem portalu Azure hello, szablony usługi Azure Resource Manager lub szablonu JSON w autonomicznych. Można określić podstawowy certyfikat i opcjonalne dodatkowej certyfikat, który jest używany do najazdy certyfikatu. Witaj certyfikatów głównych i dodatkowych, możesz określić powinien być inny niż powitania klienta administratora i określ dla certyfikatów klienta tylko do odczytu [zabezpieczeń węzeł klient](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security).

### <a name="client-to-node-security"></a>Węzeł klienta zabezpieczeń
Zabezpieczenia toonode klient jest skonfigurowany przy użyciu tożsamości klienta. tooestablish zaufania między klastrem klienta i hello, należy skonfigurować tooknow klastra hello które tożsamości klienta, które on zaufany. Można to zrobić na dwa sposoby:

-   Określ hello domeny grupy użytkowników, którzy mogą się łączyć lub
-   Określ hello domeny węzła Użytkownicy mogą łączyć.

Sieć szkieletowa usług obsługuje dwa typy kontroli różny dostęp dla klientów, które są połączone tooa klastra sieci szkieletowej usług:

-   Administrator
-   Użytkownik

Kontrola dostępu umożliwia określenie hello dla hello typy toolimit administratora klastra toocertain dostępu do operacji klastra dla różnych grup użytkowników, co klaster hello bardziej bezpieczne. Administratorzy mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu). Użytkownicy mają domyślnie tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług.

**Zabezpieczenia certyfikatów klienta do węzła**

Węzeł klient certyfikat zabezpieczeń jest skonfigurowany podczas tworzenia klastra hello za pośrednictwem portalu Azure, hello szablonów Resource Manager lub szablonu JSON autonomiczny, określając administracyjnej certyfikatu klienta i/lub certyfikatu klienta użytkownika. powitania klienta i użytkownika certyfikatów klienta administracyjnego przez użytkownika powinna być inna niż certyfikatów głównych i dodatkowych hello określone dla zabezpieczeń węzła do węzła.

Klienci łączący toohello klastra przy użyciu certyfikatu admin hello ma pełny dostęp toomanagement możliwości. Klienci łączący się za pomocą certyfikatu klienta użytkownika tylko do odczytu hello klastra toohello mają tylko możliwości toomanagement dostęp do odczytu. W innych słowa te certyfikaty służą do hello roli podstawowych kontroli dostępu (RBAC).

Dla odczytu Azure [Konfigurowanie klastra za pomocą szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) toolearn jak tooconfigure certyfikatu zabezpieczeń w klastrze.

**Węzeł Klient zabezpieczeń usługi Azure Active Directory (AAD) na platformie Azure**

Klastry z systemem Azure można również bezpieczny dostęp do punktów końcowych zarządzania toohello przy użyciu usługi Azure Active Directory (AAD). Zobacz [Konfigurowanie klastra za pomocą szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) informacji na temat jak toocreate hello niezbędne artefaktów usługi AAD, jak toopopulate ich podczas klastra tworzenie i jak tooconnect toothose klastrów później.

AAD umożliwia tooapplications dostępu użytkownika toomanage organizacji (nazywane dzierżawcy), które dzielą się na aplikacji za pomocą logowania interfejsu użytkownika sieci web i aplikacji przy użyciu środowiska macierzystego klienta.

Klaster sieci szkieletowej usług oferuje kilka tooits punktów wejścia funkcji zarządzania, w tym hello opartych na sieci web Service Fabric Explorer i Visual Studio. W związku z tym możesz utworzyć dwie usługi AAD aplikacji toocontrol dostępu toohello klastra, jednej aplikacji sieci web i jednej aplikacji natywnej.
W przypadku klastrów platformy Azure zaleca się korzystać klienci tooauthenticate zabezpieczeń usługi AAD i certyfikaty zabezpieczeń węzła do węzła.

W przypadku klastrów systemu Windows Server autonomicznych zaleca się użyć zabezpieczeń systemu Windows z kontami zarządzane przez grupę (GMA), jeśli masz system Windows Server 2012 R2 i usługi Active Directory. W przeciwnym razie nadal używać zabezpieczeń systemu Windows z konta systemu Windows.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Monitorowania i diagnostyki dla sieci szkieletowej usług Azure
[Monitorowania i diagnostyki](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) są krytyczne toodeveloping, testowania i wdrażania aplikacji i usług w każdym środowisku. Rozwiązania sieci szkieletowej usług najlepiej podczas planowanie i implementowanie monitorowania i diagnostyki, które pomagają upewnij się, aplikacji i usług działają zgodnie z oczekiwaniami w środowisku projektowym lokalnej lub w środowisku produkcyjnym.

Z punktu widzenia zabezpieczeń hello główne cele, monitorowania i diagnostyki są:

-   Wykrywanie i diagnozowanie problemów sprzętu i infrastruktury, które mogą być spowodowane tooa zdarzeń zabezpieczeń.
-   Wykrywania problemów oprogramowania i aplikacji, zapewniających wskaźnik naruszenia (Inwersja kontroli).
-   Zrozumienie zasobów toohelp zużycie zapobiec nieumyślnemu "odmowa usługi".

Witaj ogólnego przepływu pracy, monitorowania i diagnostyki obejmuje trzy kroki:

-   **Generowanie zdarzeń:** obejmuje zdarzenia (dzienników, śledzenie zdarzeń niestandardowych) zarówno w hello infrastruktury (klaster), jak i w poziomie aplikacji / usługi. Przeczytaj więcej na temat [zdarzenia na poziomie infrastruktury](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) i [zdarzenia na poziomie aplikacji](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) toounderstand jaka jest dostępna i jak tooadd dalsze instrumentacji.
-   **Agregacja zdarzeń:** generowanych zdarzeń muszą toobe zbierane i agregowane przed mogą być wyświetlane. Zazwyczaj zalecane jest używanie [diagnostyki Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (zbieranie danych dziennika na podstawie tooagent więcej podobne) lub [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (w procesie zbierania dzienników).
-   **Analiza:** zdarzeń muszą toobe wizualizowanego i jest dostępna w niektórych formatu, tooallow analizy oraz wyświetlania zgodnie z potrzebami. Istnieje kilka dużą platformy, które istnieją w rynku powitania po przejściu do analizy toohello i wizualizacja danych monitorowania i diagnostyki. Witaj dwie zalecany to [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) i [usługi Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) powodu tootheir lepszą integrację z sieci szkieletowej usług.

Można również użyć [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) toomonitor hello wielu zasobów platformy Azure, na których jest zbudowany klastra sieci szkieletowej usług.

Programu alarmowego jest oddzielny usługa można obejrzeć kondycji i obciążenie usługi i raportu kondycji dla wszystkich elementów w hierarchii modelu kondycji hello. Może to pomóc zapobiec wystąpieniu błędów, których nie można wykryć na podstawie widoku hello jednej usługi. Watchdogs są również kod toohost dobrym miejscem, który wykonuje czynności zaradczych bez interakcji z użytkownikiem (na przykład czyszczenie plików dziennika w magazynie, co pewien czas). Można znaleźć implementacji usługi programu alarmowego próbki [tutaj](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/).

## <a name="secure-using-certificates"></a>Zabezpieczenia przy użyciu certyfikatów
Za pomocą certyfikatów, informuje o tym, jak toosecure hello komunikacji między hello różnych węzłów w klastrze Windows autonomicznych, a także sposobu tooauthenticate klientów łączących się klastra toothis, za pomocą certyfikatów X.509. Dzięki temu, że tylko autoryzowani użytkownicy mogą uzyskiwać dostęp do klastra hello hello wdrożonych aplikacji i wykonywać zadania zarządzania. Certyfikat zabezpieczeń powinien być włączony w klastrze hello podczas tworzenia klastra hello.

### <a name="x509-certificates-and-service-fabric"></a>Certyfikaty X.509 i sieci szkieletowej usług
Certyfikaty cyfrowe X.509 są często używane tooauthenticate klientów i serwerów oraz tooencrypt i cyfrowego podpisywania wiadomości.

Witaj poniższej tabeli wymieniono hello certyfikaty, które będą potrzebne w konfiguracji klastra:

|Ustawienie informacji dotyczących certyfikatów |Opis|
|-------------------------------|-----------|
|ClusterCertificate|    Ten certyfikat jest wymagany toosecure hello komunikacji między węzłami hello w klastrze. Dwa różne certyfikaty, podstawowego i pomocniczego służy do uaktualnienia.|
|ServerCertificate| Ten certyfikat jest widoczne toohello klienta po próbie tooconnect toothis klastra. Do uaktualnienia, można użyć dwóch różnych certyfikatów, podstawowego i pomocniczego.|
|ClientCertificateThumbprints|  Jest to zestaw certyfikatów, które mają tooinstall na klientach hello uwierzytelniony.|
|ClientCertificateCommonNames|  Ustaw nazwa pospolita hello hello pierwszego certyfikatu klienta na powitania CertificateCommonName. Witaj CertificateIssuerThumbprint jest hello odcisk palca wystawcy hello tego certyfikatu.|
|ReverseProxyCertificate|   Jest opcjonalny certyfikat, który może być określony, jeśli chcesz, aby toosecure Twojego [wstecznego Proxy](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).|

Aby uzyskać więcej informacji na temat zabezpieczenia certyfikaty [kliknij tutaj](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security).

## <a name="role-based-access-control-rbac"></a>Kontrola dostępu oparta na rolach (RBAC)
Kontrola dostępu umożliwia hello klastra administrator toolimit dostępu toocertain klastra operacje dla różnych grup użytkowników, co klaster hello bardziej bezpieczne. Dwa typy kontroli dostępu różnych są obsługiwane dla klientów łączących się z klastrem tooa: rola administratora i roli użytkownika.

Administratorzy mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu). Użytkownicy mają domyślnie tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług.

Można określić hello administratora i użytkownika klienta role w czasie tworzenia klastra hello podając oddzielne tożsamości (certyfikaty, AAD itp.) dla każdego. Aby uzyskać więcej informacji na hello domyślne uprawnienia kontroli dostępu i jak toochange hello domyślnych ustawień, zobacz [kontrola dostępu oparta na rolach dla klientów usługi sieć szkieletowa](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

## <a name="secure-standalone-cluster-using-windows-security"></a>Zabezpieczanie klastra autonomiczny przy użyciu zabezpieczeń systemu Windows
tooprevent nieautoryzowany klastra usługi sieć szkieletowa tooa dostępu, należy zabezpieczyć hello klastra. Bezpieczeństwa jest szczególnie ważne, uruchomienie klastra hello obciążeń produkcyjnych. Opisuje sposób tooconfigure węzła do węzła i węzeł klient zabezpieczeń przy użyciu zabezpieczeń systemu Windows w hello pliku w pliku ClusterConfig.JSON.

**Konfigurowanie zabezpieczeń systemu Windows przy użyciu usługi zarządzane przez grupę**

Węzeł toonode zabezpieczeń jest skonfigurowana przez ustawienie [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) gdy sieć szkieletowa usług musi toorun mocy przez grupę. W kolejności toobuild relacje zaufania między węzłami ich należy pamiętać o sobie nawzajem.

Zabezpieczenia toonode klient jest skonfigurowany przy użyciu ClientIdentities. W kolejności tooestablish relacji zaufania między klienta i hello klastra należy skonfigurować tooknow klastra hello które tożsamości klienta, które on zaufany.

**Konfigurowanie zabezpieczeń systemu Windows przy użyciu grupy na komputerze**

Węzeł toonode zabezpieczeń jest konfigurowane przez ustawienie za pomocą ClusterIdentity, jeśli chcesz, aby toouse grupy na komputerze w ramach domeny usługi Active Directory. Aby uzyskać więcej informacji, zobacz [Utwórz grupę maszyny w usłudze Active Directory](https://msdn.microsoft.com/library/aa545347).

Węzeł Klient zabezpieczeń jest konfigurowana przy użyciu ClientIdentities. tooestablish zaufania między klastrem klienta i hello, musisz skonfigurować hello klastra tooknow powitania klienta tożsamości, które hello klastra można ufać. Można ustanowić relacji zaufania na dwa sposoby:

-   Określ hello domeny grupy użytkowników, które mogą nawiązywać połączenia.
-   Określ hello domeny węzła Użytkownicy mogą łączyć.

## <a name="configure-application-security-in-service-fabric"></a>Konfigurowanie zabezpieczeń aplikacji w sieci szkieletowej usług
### <a name="managing-secrets-in-service-fabric-applications"></a>Zarządzanie kluczy tajnych w aplikacji sieci szkieletowej usług
Ta metoda ułatwia zarządzanie kluczy tajnych w aplikacji sieci szkieletowej usług. Klucze tajne można poufne informacje, takie jak parametry połączenia magazynu, hasła lub inne wartości, które nie powinny być traktowane w postaci zwykłego tekstu.

Ta metoda używa [usługi Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) toomanage kluczy i kluczy tajnych. Jednak przy użyciu kluczy tajnych w aplikacji jest hostowane w dowolnym miejscu chmury tooallow niezależny od platformy aplikacji wdrożonych toobe tooa klastra. W tym przepływie istnieją cztery główne kroki:

-   Uzyskaj certyfikat Szyfrowanie danych.
-   Zainstaluj certyfikat hello w klastrze.
-   Szyfrowanie tajny wartości podczas wdrażania aplikacji przy użyciu certyfikatu hello i wstawić je do pliku konfiguracji Settings.xml usługi.
-   Odczyt zaszyfrowanych wartości poza Settings.xml w tym celu odszyfrowuje z hello tego samego certyfikatu szyfrowanie.

>[!Note]
>Dowiedz się więcej o [Zarządzanie kluczy tajnych w aplikacji usługi Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="configure-security-policies-for-your-application"></a>Konfigurowanie zasad zabezpieczeń aplikacji
Przy użyciu zabezpieczeń sieci szkieletowej usług Azure, możesz pomóc bezpiecznych aplikacji uruchomionych w klastrze hello w obszarze konta innego użytkownika. Usługa sieci szkieletowej zabezpieczeń pomaga również w hello bezpiecznych zasobów, które są używane przez aplikacje w czasie hello wdrożenia na kontach użytkowników hello — na przykład, plików, katalogów i certyfikatów. Dzięki temu uruchamianie aplikacji, nawet w środowisku hostowanej udostępnionego bardziej bezpieczne od siebie nawzajem.
Witaj kroki obejmują:

-   Skonfiguruj zasady powitania dla punktu wejścia instalacji usługi.
-   Uruchom polecenia programu PowerShell z punktu wejścia instalacji.
-   Użyj konsoli dla debugowania lokalnego.
-   Konfigurowanie zasad dla pakietów kodu usługi.
-   Przypisać zasady zabezpieczeń dostępu dla punktów końcowych HTTP i HTTPS.

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Bezpiecznej komunikacji dla usług w sieci szkieletowej usług Azure zabezpieczeń
Zabezpieczeń jest jednym z najważniejszych aspektów komunikacji hello. Struktura aplikacji Hello niezawodne usługi zapewnia kilka stosy wbudowane komunikacji i narzędzi, które mogą być używane tooimprove zabezpieczeń.

-   [Zabezpieczanie usługi podczas korzystania z usług zdalnych](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication).
-   [Zabezpieczanie usługi podczas korzystania z stosu komunikacji WCF](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack).

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać ogólne informacje o zabezpieczeniach klastra, zobacz [utworzyć klaster na platformie Azure przy użyciu szablonu usługi Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) i [portalu Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal).
- Dowiedz się więcej, zobacz [zabezpieczeń klastra sieci szkieletowej usług](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security).
