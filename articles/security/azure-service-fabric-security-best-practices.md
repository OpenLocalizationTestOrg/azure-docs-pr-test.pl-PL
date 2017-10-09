---
title: "aaaAzure sieci szkieletowej usług najlepsze rozwiązania w zakresie zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera zestaw najlepsze rozwiązania dotyczące zabezpieczeń sieć szkieletowa usług Azure."
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
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Azure Service Fabric najlepszych rozwiązań dotyczących zabezpieczeń
Wdrażanie aplikacji na platformie Azure jest szybkie, łatwe i ekonomiczne. Przed wdrożeniem aplikacji w chmurze w produkcji toohave przydatne najlepszym rozwiązaniem tooassist podczas obliczania aplikacja z listą ważne i zalecane najlepsze rozwiązania.

Sieć szkieletowa usług Azure to platforma systemów rozproszonych, dzięki którym toopackage łatwe, wdrażanie i zarządzanie mikrousług skalowalne i niezawodne. Sieć szkieletowa usług dotyczy również hello znaczne trudności w tworzenie i zarządzanie aplikacjami w chmurze. Deweloperzy i administratorzy mogą uniknąć złożonych problemów związanych z infrastrukturą i skoncentrować się na implementowaniu wymagających obciążeń o znaczeniu strategicznym, które są skalowalne, niezawodne i łatwe w zarządzaniu. 

Dla każdego najlepszym rozwiązaniem prezentujemy zasady:

-   Jakie hello najlepszym rozwiązaniem jest
-   Dlaczego chcesz tooenable tej najlepsze praktyki
-   Co może wynikać hello tooenable hello najlepszym rozwiązaniem w przeciwnym przypadku
-   Jak można znaleźć tooenable hello najlepsze praktyki

Obecnie istnieją hello następujące najlepsze rozwiązania sieć szkieletowa usług Azure:

-   Użyj szablonu usługi Azure Resource Manager (ARM) i bezpieczne klastra toocreate modułu programu PowerShell Azure sieci szkieletowej usług
-   Użyj certyfikatów X.509
-   Konfigurowania zasad zabezpieczeń
-   Niezawodne podmiotów zabezpieczeń konfiguracji
-   Konfigurowanie protokołu SSL dla usługi Azure Service Fabric
-   Izolacja sieci/zabezpieczeń z usługi Azure Service Fabric
-   Konfigurowanie magazynu kluczy dla zabezpieczeń
-   Przypisywanie użytkowników tooroles


## <a name="best-practices-for-securing-your-cluster"></a>Najlepsze rozwiązania dotyczące zabezpieczania klastra

**Duży obraz**

Zawsze używaj bezpiecznej klastra
-   Klaster zabezpieczeń — korzystają z certyfikatów
-   Dostęp klienta (Admin i tylko do odczytu) — Użyj usługi AAD

Użyj zautomatyzowanych wdrożeń
-   Użyj toogenerate skrypty, wdrażanie i kluczy tajnych są przerzucane
-   Zachowaj hello kluczy tajnych w KV, dla każdego dostępu klienta przy użyciu usługi AD
-   Ludzkich nie powinny mieć dostępu toothem bez uwierzytelniania.

Ponadto należy wziąć pod uwagę następujące hello:
-   Tworzenie sieci DMZ przy użyciu grup zabezpieczeń sieci (NSG)
-   Użyj tooRDP serwery przeskoku do maszyn wirtualnych klastra lub toomanage klastra

Klastry muszą być użytkownikami zabezpieczonych tooprevent nieautoryzowany łączenie tooyour klastra, szczególnie w przypadku, gdy ma na nim uruchomione obciążeń produkcyjnych. Możliwe toocreate niezabezpieczona klastra, ale dzięki temu tooit tooconnect użytkowników anonimowych, jeśli eksponuje toohello punkty końcowe zarządzania publicznej sieci Internet.

Używać technologii tooimplement tych scenariuszy. Witaj [klastra scenariusze zabezpieczeń](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) są:

-   Węzła do węzła zabezpieczeń ta zabezpiecza komunikację między hello maszyn wirtualnych i komputerów w klastrze hello. Daje to pewność, że tylko komputery, które są autoryzowane toojoin hello klastra mogą uczestniczyć w hosting aplikacji i usług w klastrze hello.
Klastry z systemem Azure lub autonomiczne klastry z systemem Windows można użyć dowolnego [certyfikatu zabezpieczeń](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security) lub [zabezpieczenia systemu Windows](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security) dla komputerów z systemem Windows Server.
-   Węzeł Klient zabezpieczeń ta zabezpiecza komunikację między klienta sieci szkieletowej usług oraz poszczególnych węzłów w klastrze hello.
-   Kontrola dostępu oparta na rolach (RBAC) - określonej role klient hello administratora i użytkownika w czasie tworzenia klastra hello przez podanie oddzielne tożsamości (certyfikaty, AAD itp.) dla każdego.
-   Zalecenia dotyczące zabezpieczeń — klastrów dla usługi Azure, zaleca się korzystanie z klientów tooauthenticate zabezpieczeń usługi AAD i certyfikaty zabezpieczeń węzła do węzła.

autonomiczny hello tooconfigure klastra systemu Windows, zobacz [konfigurowania ustawień dla klastra systemu windows autonomiczny](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest).

Za pomocą szablonów usługi Azure Resource Manager i usługi sieci szkieletowej Azure PowerShell modułu toocreate bezpiecznego klastra.
Przeszukiwań przewodnik krok po kroku, możesz skonfigurować bezpiecznego sieć szkieletowa usług Azure klastra na platformie Azure przy użyciu usługi Azure Resource Manager jest dostępna [tutaj](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm).

Użyj toocustomize szablonu usługi Azure Resource Manager hello klastra
-   Zarządzane ustawienia magazynu dla wirtualnych dysków twardych maszyny Wirtualnej

Użyj hello Azure Resource Manager szablonu toodrive zmiany tooyour grupy zasobów
-   Łatwość konfiguracji zarządzania
-   Inspekcja

Traktuj konfiguracji klastra jako kod
-   Można dokładnego sprawdzania konfiguracji hello wybierz toodeploy
-   Należy unikać tootweak polecenia niejawne zasobów bezpośrednio

Wiele aspektów hello [cyklem życia aplikacji usługi sieć szkieletowa](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle) można zautomatyzować. [Usługa sieci szkieletowej Azure PowerShell modułu](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package) zautomatyzowanie typowych zadań związanych z wdrażanie, uaktualnianie, usuwanie i testowanie aplikacji sieci szkieletowej usług Azure. Zarządzane i dostępne są również interfejsy API protokołu HTTP do zarządzania aplikacjami.

## <a name="use-x509-certificates"></a>Użyj certyfikatów X.509
Klastry zawsze być zabezpieczone za pomocą certyfikatów X.509 lub zabezpieczenia systemu Windows. Zabezpieczeń jest skonfigurowany tylko w czasie tworzenia klastra i nie jest możliwe tooenable zabezpieczeń po utworzeniu klastra hello.

W przypadku określania [certyfikatu klastra](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security), ustaw wartość hello ClusterCredentialType tooX509. W przypadku określania certyfikatu serwera dla połączeń zewnętrznych, należy ustawić hello ServerCredentialType tooX509.

-   Certyfikatów używanych w klastrach z systemem obciążeń produkcyjnych powinna być utworzony przy użyciu poprawnie skonfigurowanej usługi certyfikatów systemu Windows Server lub uzyskane z zatwierdzonych certyfikatu urzędu certyfikacji.
-   Nigdy nie używaj żadnych tymczasowej lub certyfikaty testów w środowisku produkcyjnym, które są tworzone za pomocą narzędzi, takich jak MakeCert.exe.
-   Można użyć certyfikatu z podpisem własnym, ale powinien tylko zrobić dla klastrów testowych, a nie w środowisku produkcyjnym.

Jeśli klaster hello jest niebezpieczne. Każda osoba może połączyć się z nim anonimowo i przeprowadzić operacje związane z zarządzaniem. Dlatego też klastry produkcyjne należy zawsze zabezpieczać przy użyciu certyfikatów X.509 lub zabezpieczeń systemu Windows.

toolearn więcej jak wyświetlić certyfikaty tooenable klastra sieci szkieletowej usług, [Dodaj lub Usuń certyfikaty dla klastra sieci szkieletowej usług](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure).

## <a name="configure-security-policies"></a>Konfigurowania zasad zabezpieczeń
Sieć szkieletowa usług pomaga również hello bezpiecznych zasobów, które są używane przez aplikacje w czasie hello wdrożenia na kontach użytkowników hello — na przykład, plików, katalogów i certyfikatów. Dzięki temu uruchamianie aplikacji, nawet w środowisku hostowanej udostępnionego bardziej bezpieczne od siebie nawzajem.

-   Użyj grupy domeny usługi Active Directory lub użytkownika: można uruchomić usługi hello hello poświadczenia dla konta użytkownika lub grupy usługi Active Directory. To jest usługa Active Directory lokalnie w domenie, a nie z usługą Azure Active Directory (Azure AD). Przy użyciu użytkownika domeny lub grupy, można następnie dostęp do innych zasobów w domenie hello (na przykład udziałów plików), które ma odpowiednie uprawnienia.

-   Przypisać zasady zabezpieczeń dostępu dla punktów końcowych HTTP i HTTPS: manifest usługi hello deklaruje punktu końcowego zasobów przy użyciu protokołu hello HTTP zastosowania usługi tooa zasad RunAs, należy określić tooensure SecurityAccessPolicy, że porty przydzielone toothese punkty końcowe są poprawnie dostępu kontrolowane przez wymienione hello konto użytkownika Uruchom jako, które jest uruchamiana usługa hello. W przeciwnym razie http.sys nie ma dostępu do usługi toohello i uzyskać awarii przy wywołaniach z powitania klienta.
toolearn więcej włączyć zasady zabezpieczeń w usługi sieci szkieletowej, zobacz temat [konfigurowania zasad zabezpieczeń dla aplikacji](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security).

## <a name="reliable-actors-security-configuration"></a>Niezawodne podmiotów zabezpieczeń konfiguracji
Usługa sieci szkieletowej Reliable Actors jest implementacją wzorca projektowego hello aktora. Podobnie jak w przypadku dowolnego wzorcu projektowym oprogramowania hello decyzję, czy toouse określony wzorzec jest wykonywana w oparciu czy oprogramowania projektowania problem pasuje do wzorca hello.

Stanowią ogólne wskazówki należy wziąć pod uwagę toomodel wzorca aktora hello problemów lub scenariuszu jeśli:
-   Obszar problem obejmuje dużą liczbą (tysięcy lub więcej) jednostek mały, niezależne i izolowane stanu i logiki.
-   Ma toowork z jednowątkowego obiektów, które nie wymagają znaczących interakcji z zewnętrznego składników, w tym badania stanu zestawu podmiotów.
-   Swoich wystąpień aktora nie zablokuje wywołań nieprzewidywalne opóźnień wysyłając operacji We/Wy.

W sieci szkieletowej usług, złośliwych użytkowników zostały wdrożone w ramach Reliable Actors hello: struktura aplikacji na podstawie wzorca aktora wbudowane nad [niezawodne usługi sieć szkieletowa usług](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction). Każdej usługi niezawodnego aktora, jaki jest rzeczywiście podzielonym na partycje, stanowe niezawodnej usługi.
Każdy aktora jest zdefiniowany jako wystąpienie typu aktora, sposób identyczne toohello obiektu .NET jest wystąpieniem typu .NET. Na przykład może to być typ aktora, która implementuje funkcje hello kalkulatora i może istnieć wiele podmiotów tego typu rozproszonych w różnych węzłach w klastrze. Każdy taki aktora jest unikatowo identyfikowana przez identyfikator aktora.

[Konfiguracje zabezpieczeń replikatora](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration) są używane toosecure kanał komunikacyjny hello, używaną podczas replikacji. Oznacza to, czy usługi nie widzi siebie nawzajem ruch związany z replikacją, zapewnia, że dane hello jest zyskuje dużą dostępność również jest bezpieczne. Domyślnie puste zabezpieczeń sekcji konfiguracji uniemożliwia zabezpieczeń replikacji.
Konfiguracje replikatora skonfiguruj replikatora hello, odpowiedzialną za tworzenie stanu dostawcy stanu aktora hello wysoce niezawodne.

## <a name="configure-ssl-for-azure-service-fabric"></a>Konfigurowanie protokołu SSL dla usługi Azure Service Fabric

Uwierzytelnianie serwera: [podczas](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) hello klastra zarządzania punkty końcowe tooa zarządzania klienta, aby hello klienta zarządzania znała jest mówić toohello rzeczywistych klastra. Ten certyfikat zawiera również [SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) hello interfejsu API zarządzania HTTPS i Service Fabric Explorer za pośrednictwem protokołu HTTPS.
Należy uzyskać niestandardowej nazwy domeny dla klastra. Podczas żądania certyfikatu z urzędu certyfikacji, hello nazwa podmiotu certyfikatu musi odpowiadać hello niestandardowej nazwy domeny używanej dla klastra.

tooconfigure protokołu SSL dla aplikacji, należy najpierw tooget certyfikat SSL, który został podpisany przez urząd certyfikacji, zaufanych innej firmy, który wystawia certyfikaty w tym celu. Jeśli nie masz już jeden, należy tooobtain jedną z firmy, która sprzedaje certyfikatów SSL.

Hello certyfikatu musi spełniać następujące wymagania dotyczące certyfikatów SSL na platformie Azure hello:
-   Witaj, certyfikat musi zawierać klucz prywatny.
-   Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, można eksportować tooa plik wymiany informacji osobistych (pfx).
-   Hello nazwa podmiotu certyfikatu musi odpowiadać usługi hello tooaccess hello domeny użytej w chmurze. Nie można uzyskać certyfikatu SSL z urzędu certyfikacji (CA) dla domeny cloudapp.net hello. Należy uzyskać toouse nazwy domeny niestandardowej podczas dostępu usługi. Podczas żądania certyfikatu z urzędu certyfikacji, nazwa podmiotu certyfikatu hello musi odpowiadać hello domenę niestandardową nazwę używaną tooaccess aplikacji. Na przykład z niestandardowej nazwy domeny to contoso.com spowoduje zażądanie certyfikatu z urzędu certyfikacji dla **. contoso.com** lub **www.contoso.com.**
-   Witaj certyfikatu należy użyć co najmniej 2048-bitowego szyfrowania.

HTTP jest niebezpieczne i ataków tooeavesdropping podmiotu ponieważ hello przesyłane z serwera sieci web toohello przeglądarki sieci web hello lub między innymi punktami końcowymi, dane są przesyłane w postaci zwykłego tekstu. Oznacza to, osoby atakujące mogą przechwytywać i poufnych danych, takich jak karty kredytowej i konta logowania. Gdy dane są wysyłane lub opublikowane za pośrednictwem przeglądarki przy użyciu protokołu HTTPS, SSL zapewnia, że takie informacje są szyfrowane i chronione przed przechwyceniem.

więcej, zobacz temat toolearn [skonfigurować protokół SSL dla aplikacji azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate).

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Izolacja sieci/zabezpieczeń z usługi Azure Service Fabric
Użyj [szablonu usługi Azure Resource Manager (ARM)](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) jako przykład konfigurowania trzy nodetype bezpiecznego klastra i toocontrol hello ruchu przychodzącego i wychodzącego ruchu sieciowego przy użyciu grup zabezpieczeń sieci.

Szablon Hello ma grupy zabezpieczeń sieci dla każdego hello maszyny wirtualnej skali set(VMSS) toocontrol hello ruch do i z hello VMSS. Domyślnie zasady hello są konfigurowane tooallow wszystkie hello ruch wymagany przez hello systemu usług i hello aplikacji porty określone w szablonie hello. Przejrzyj te reguły i dokonać zmiany toofit potrzeb, w tym dodawanie nowych użytkowników dla aplikacji.

Aby uzyskać więcej informacji, zobacz [Azure Service Fabric — typowe scenariusze sieci](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking).

## <a name="set-up-a-key-vault-for-security"></a>Konfigurowanie magazynu kluczy dla zabezpieczeń
Certyfikaty są używane w sieci szkieletowej usług tooprovide uwierzytelnianie i szyfrowanie toosecure różnych aspektów klastra i jego zastosowań.

Sieć szkieletowa usług używa toosecure certyfikatów X.509 klastra i zapewnia funkcje zabezpieczeń aplikacji. Za pomocą usługi Key Vault[zarządzanie certyfikatami](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure) dla klastrów sieci szkieletowej usług platformy Azure. Po wdrożeniu klastra w systemie Azure hello dostawcy zasobów platformy Azure, który jest odpowiedzialny za tworzenie klastrów usługi sieć szkieletowa ściąga certyfikaty z magazynu kluczy i instaluje je w klastrze hello maszyn wirtualnych.

Relacja między Hello [usługi Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), klastra sieci szkieletowej usług i hello dostawcy zasobów platformy Azure, który wykorzystuje certyfikaty przechowywane w magazynie kluczy, podczas tworzenia klastra.

**Utwórz grupę zasobów** hello pierwszym krokiem jest toocreate grupę zasobów, w szczególności dla magazynu kluczy. Firma Microsoft zaleca umieścić hello magazynu kluczy w jego własnej grupy zasobów. Ta akcja umożliwia usunięcie hello obliczeniowej i pamięci masowej grup zasobów, tym hello grupy zasobów, zawierającą klaster sieci szkieletowej usług bez utraty z kluczy i kluczy tajnych. Witaj grupę zasobów, która zawiera magazynu kluczy musi należeć do hello hello klastra, który go używa tego samego regionu.

**Tworzenie magazynu kluczy w nowej grupy zasobów hello** hello magazynu kluczy musi być włączona dla wdrożenia tooallow hello certyfikaty tooget dostawcy zasobów obliczeniowych od niego i zainstalować ją na wystąpieniu maszyny wirtualnej.
toolearn więcej jak wyświetlić tooset się usługi Azure key vault, [wprowadzenie do usługi Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started).

## <a name="assign-users-roles"></a>Przypisz role użytkowników
Po utworzeniu toorepresent aplikacji hello klastra, przypisywanie użytkownikom ról toohello obsługiwane przez usługi Service Fabric: tylko do odczytu i administratora. Można przypisać role hello za pomocą hello klasycznego portalu Azure.

>[!Note]
> Aby uzyskać więcej informacji na temat ról w sieci szkieletowej usług, zobacz [kontroli dostępu opartej na rolach dla klientów usługi sieć szkieletowa](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

Sieć szkieletowa usług Azure obsługuje dwa typy kontroli różny dostęp dla klientów, które są połączone tooa [klastra sieci szkieletowej usług](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm): administratora i użytkownika. Kontrola dostępu umożliwia hello klastra administrator toolimit dostępu toocertain klastra operacje dla różnych grup użytkowników, co klaster hello bardziej bezpieczne.

## <a name="next-steps"></a>Następne kroki
- Konfigurowanie sieci szkieletowej usług [środowisko projektowe](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started).
- Dowiedz się więcej o [opcje pomocy technicznej usługi sieć szkieletowa](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).

