---
title: "aaaSet się ciągłej integracji dla platformy Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Zapoznaj się z omówieniem jak tooset ciągłej integracji i wdrażania aplikacji sieci szkieletowej usług za pomocą programu Visual Studio Team Services (VSTS)."
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>Konfigurowanie usługi sieć szkieletowa ciągłej integracji i wdrażanie za pomocą programu Visual Studio Team Services
W tym artykule opisano hello tooset kroków ciągłej integracji i wdrażania aplikacji sieci szkieletowej usług Azure za pomocą programu Visual Studio Team Services (VSTS).

Ten dokument odzwierciedla bieżącą procedurę hello i jest oczekiwany toochange wraz z upływem czasu.

## <a name="prerequisites"></a>Wymagania wstępne
tooget pracę, wykonaj następujące kroki:

1. Upewnij się, że masz konto usługi Team Services tooa dostępu lub [utworzyć](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) samodzielnie.
2. Upewnij się, że masz projektu zespołowego Team Services tooa dostępu lub [utworzyć](https://www.visualstudio.com/docs/setup-admin/create-team-project) samodzielnie.
3. Upewnij się, że masz toowhich klastra sieci szkieletowej usług można wdrożyć aplikację lub utworzyć przy użyciu hello [portalu Azure](service-fabric-cluster-creation-via-portal.md), [szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md), lub [programu Visual Studio ](service-fabric-cluster-creation-via-visual-studio.md).
4. Upewnij się, że utworzono już projektu aplikacji sieci szkieletowej usług (.sfproj). Projekt, który został utworzony lub uaktualniony przy użyciu usługi sieci szkieletowej SDK 2.1 lub wyższej musi być (hello .sfproj plik powinien zawierać wartość właściwości ProjectVersion 1.1 lub nowszej).

> [!NOTE]
> Agenci kompilacji niestandardowej nie są już wymagane. Zespół usługi hostowanej agentów, teraz są zainstalowane z oprogramowania do zarządzania klastrami usługi Service Fabric, co pozwala na wdrożenie aplikacji bezpośrednio z tych agentów.
> 
> 

## <a name="configure-and-share-your-source-files"></a>Konfigurowanie i udostępnianie plików źródłowych
Hello pierwsza rzecz, którą chcesz toodo jest przygotowanie profilu publikowania do użytku przez proces wdrażania hello wykonywanego Team Services.  profil publikowania Hello powinna być tootarget skonfigurowanych hello klastra, które zostały wcześniej przygotowane:

1. Wybierz profil publikowania w ramach projektu aplikacji ma toouse przepływu pracy ciągłej integracji. Wykonaj hello [publikowania instrukcje](service-fabric-publish-app-remote-cluster.md) na temat toopublish aplikacji tooa zdalnego klastra. Faktycznie niepotrzebne toopublish aplikacji jednak. Możesz kliknąć hello **zapisać** hiperłącze w powitania po skonfigurowaniu rzeczy odpowiednio okna dialogowego publikowania.
2. Jeśli chcesz, aby Twoje toobe aplikacji uaktualnione każdego wdrożenia, znajdującego się w Team Services, ma tooconfigure hello uaktualniania tooenable profilu publikowania. W hello okna dialogowego używane sam publikowania w kroku 1, upewnij się, że hello **hello uaktualniania aplikacji** jest zaznaczone pole wyboru.  Dowiedz się więcej o [Konfigurowanie dodatkowych ustawień uaktualnienia](service-fabric-visualstudio-configure-upgrade.md). Kliknij przycisk hello **zapisać** hyperlink toosave hello ustawienia toohello profilu publikowania.
3. Sprawdź, czy zapisano zmiany publikowania toohello profilu i Anuluj hello okna dialogowego publikowania.
4. Teraz nadszedł czas zbyt[udziału plików źródłowych projektu aplikacji](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) z usługi Team Services. Gdy plików źródłowych są dostępne w usłudze Team Services, możesz teraz przejść na kolejny krok toohello generowania kompilacji. 

## <a name="create-a-build-definition"></a>Tworzenie definicji kompilacji
Definicja kompilacji Team Services zawiera opis przepływu pracy, który składa się z zestaw kroków kompilacji, które są wykonywane sekwencyjnie. Celem Hello hello definicji kompilacji, tworzona jest tooproduce pakiet aplikacji sieci szkieletowej usług i innych artefaktów, które mogą być używane toodeploy aplikacji hello. Dowiedz się więcej na temat usługi Team Services [definicje kompilacji](https://www.visualstudio.com/docs/build/define/create).

### <a name="create-a-definition-from-hello-build-template"></a>Utwórz definicję hello budowania szablonu
1. Otwórz projekt w programie Visual Studio Team Services.
2. Wybierz hello **kompilacji** kartę.
3. Wybierz hello zielony  **+**  zarejestrować toocreate nową definicję kompilacji.
4. Witaj zostanie otwarte okno dialogowe, wybierz **aplikacji sieci szkieletowej usług Azure** w hello **kompilacji** kategorii szablonu.
5. Wybierz **dalej**.
6. Wybierz hello repozytorium i gałęzi skojarzone z aplikacją sieci szkieletowej usług.
7. Wybierz kolejki agenta hello mają toouse. Hostowani agenci są obsługiwane.
8. Wybierz pozycję **Utwórz**.
9. Zapisz definicję kompilacji hello i podaj nazwę.
10. Witaj następujący ustęp znajduje się opis kroków kompilacji hello generowane przez szablon hello:

| Krok kompilacji | Opis |
| --- | --- |
| Przywracanie NuGet |Przywraca hello pakietów NuGet dla rozwiązania hello. |
| Tworzenie rozwiązania \*.sln |Tworzy hello całego rozwiązania. |
| Tworzenie rozwiązania \*.sfproj |Generuje hello pakiet aplikacji sieci szkieletowej usług, który jest aplikacja hello toodeploy używane. lokalizacja pakietu aplikacji Hello jest określony toobe w katalogu artefaktów kompilacji hello. |
| Aktualizuj wersje aplikacji sieci szkieletowej usług |Aktualizuje hello wersji wartości zawartych w tooallow pliki manifestu pakietu aplikacji hello uaktualnienia pomocy technicznej. Zobacz hello [stronę dokumentacji zadań](https://go.microsoft.com/fwlink/?LinkId=820529) Aby uzyskać więcej informacji. |
| Skopiuj pliki |Kopie hello opublikować profilu i parametry plików toohello kompilację aplikacji w artefakty toobe używane dla wdrożenia. |
| Publikowanie artefaktów |Publikuje artefakty hello kompilacji. Pozwala na określenie wersji kompilacji hello tooconsume artefaktów. |

### <a name="verify-hello-default-set-of-tasks"></a>Sprawdź hello domyślny zestaw zadań
1. Sprawdź hello **rozwiązania** pole wejściowe dla hello **Przywracanie NuGet** i **zbudować rozwiązanie** kroki procesu kompilacji.  Domyślnie te kroki procesu kompilacji wykonać na wszystkich plików rozwiązania, które znajdują się w repozytorium hello skojarzone.  Jeśli chcesz tylko toooperate definicji kompilacji hello na jednym z tych plików rozwiązania, należy tooexplicitly aktualizacji hello ścieżki toothat pliku.
2. Sprawdź hello **rozwiązania** pole wejściowe dla hello **pakietu aplikacji** kroku kompilacji.  Domyślnie ten krok kompilacji przyjęto założenie, że tylko jeden projekt aplikacji sieci szkieletowej usług (.sfproj) istnieje w repozytorium hello.  Jeśli masz wiele takich plików w repozytorium i chcesz tootarget tylko jeden z nich dla tej definicji kompilacji, należy tooexplicitly aktualizacji hello ścieżki toothat pliku.  Jeśli chcesz toopackage aplikacji wielu projektów w repozytorium, należy toocreate dodatkowe **kompilacji programu Visual Studio** czynnościach w ramach definicji kompilacji hello, że każdy docelowy projekt aplikacji.  Następnie musisz także tooupdate hello **argumenty programu MSBuild** pola dla każdego z tych kroki procesu kompilacji, tak aby hello lokalizacja pakietu jest unikatowy dla każdego z nich.
3. Sprawdź hello versioning zachowanie zdefiniowane w hello **wersje aplikacji sieci szkieletowej usług aktualizacji** kroku kompilacji.  Domyślnie ten krok kompilacji, dołącza hello kompilacji tooall wersji wartości liczbowe w plikach manifestu pakietu aplikacji hello. Zobacz hello [stronę dokumentacji zadań](https://go.microsoft.com/fwlink/?LinkId=820529) Aby uzyskać więcej informacji. Jest to przydatne do obsługi uaktualniania aplikacji, ponieważ każdego wdrożenia uaktualnienia wymaga wartości innej wersji z hello poprzedniego wdrożenia. Jeśli nie jest pomyślny przebieg toouse uaktualniania aplikacji, w przepływie pracy, można rozważyć wyłączenie tego kroku kompilacji. Musi być wyłączony, jeśli masz zamiar tooproduce kompilacji, które mogą być używane toooverwrite istniejącej aplikacji sieci szkieletowej usług. Witaj, wdrożenie zakończy się niepowodzeniem, jeśli hello wersję aplikacji hello utworzony przez kompilację hello jest niezgodna z wersją hello aplikacji hello w klastrze hello.
4. Jeśli rozwiązanie zawiera projekt .NET Core, musi upewnij się, że definicję kompilacji zawiera kroku kompilacji, która przywraca hello zależności:
   1. Wybierz **Dodaj krok kompilacji...** .
   2. Zlokalizuj hello **wiersza polecenia** zadań na karcie Narzędzia hello, a następnie kliknij przycisk Dodaj.
   3. Dla pól wejściowych hello zadań użyj hello następujące wartości:
   4. Narzędzie: dotnet
   5. Argumenty: Przywracanie
   6. Przeciągnij hello zadań tak, aby natychmiast po hello **Przywracanie NuGet** kroku.
5. Zapisz zmiany wprowadzone toohello definicji kompilacji.

### <a name="try-it"></a>Wypróbuj
Wybierz **kolejka kompilacji** toomanually uruchomić kompilacji. Opisano również wyzwalacze wypychania lub zaewidencjonowania. Po upewnieniu się pomyślnie wykonuje hello kompilacji, możesz teraz przejść na toodefining definicji wersji, która wdraża klaster tooa aplikacji.

## <a name="create-a-release-definition"></a>Utwórz definicję zlecenia
Definicja wersji Team Services zawiera opis przepływu pracy, który składa się z zestawu zadań, które są wykonywane sekwencyjnie. Celem Hello hello definicji wersji, tworzona jest tootake pakietu aplikacji i wdrożyć ją tooa klastra. Razem hello definicję kompilacji i definicji wersji można wykonywać hello całego przepływu pracy z począwszy od źródła tooending plików przy użyciu aplikacji uruchomionych w klastrze. Dowiedz się więcej na temat usługi Team Services [wersji definicji](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).

### <a name="create-a-definition-from-hello-release-template"></a>Utwórz definicję hello wersji szablonu
1. Otwórz projekt w programie Visual Studio Team Services.
2. Wybierz hello **wersji** kartę.
3. Wybierz hello zielony  **+**  zarejestrować toocreate nowej definicji wersji, a następnie wybierz **Tworzenie wersji definicji** hello menu.
4. Witaj zostanie otwarte okno dialogowe, wybierz **wdrażania usługi Azure Service Fabric** w hello **wdrożenia** kategorii szablonu.
5. Wybierz **dalej**.
6. Wybierz definicję kompilacji hello ma toouse jako źródło hello tej definicji wersji.  Definicja kompilacji systemu Hello wersji definicji odwołania hello artefakty oferowanych przez hello wybrane.
7. Sprawdź hello **ciągłe wdrażanie** pole wyboru, jeśli chcesz, aby toohave Team Services automatycznie utworzyć nową wersję i wdrażanie aplikacji usługi Service Fabric hello zawsze, gdy kompilacja zostaje ukończona.
8. Wybierz kolejki agenta hello mają toouse. Hostowani agenci są obsługiwane.
9. Wybierz pozycję **Utwórz**.
10. Edytuj nazwę definicji hello, klikając ikonę ołówka hello u góry hello hello strony.
11. Wybierz hello toowhich klastra należy wdrożyć aplikację z hello **połączenia klastra** pola wejściowego hello zadania. połączenia klastra Hello zawiera hello niezbędne informacje, które umożliwia hello wdrożenia zadania tooconnect toohello klastra. Jeśli połączenie klastra nie jest jeszcze ma dla klastra, wybierz hello **Zarządzaj** hyperlink dalej toohello pola tooadd jeden. Na stronie powitania, którego kliknięcie spowoduje otwarcie wykonaj hello następujące kroki:
    1. Wybierz **nowy punkt końcowy usługi** , a następnie wybierz **sieć szkieletowa usług Azure** hello menu.
    2. Wybierz typ uwierzytelniania używany przez klaster hello docelowe przez ten punkt końcowy hello.
    3. Zdefiniuj nazwę połączenia w hello **nazwa połączenia** pola.  Zazwyczaj użyje hello nazwy klastra.
    4. Zdefiniuj hello adres URL punktu końcowego połączenia dla klienta w hello **punktu końcowego klastra** pola.  Przykład: tcp://contoso.westus.cloudapp.azure.com:19000.
    5. Dla poświadczeń usługi Azure Active Directory, należy zdefiniować hello poświadczenia mają toouse tooconnect toohello klastra w hello **Username** i **hasło** pola.
    6. Do uwierzytelniania na podstawie certyfikatu, zdefiniuj hello Base64 kodowanie pliku z certyfikatem klienta hello w hello **certyfikatu klienta** pola.  Zobacz hello pomocy w oknie podręcznym o to pole, aby uzyskać informacje na temat tooget, że wartość.  Jeśli certyfikat jest chroniony hasłem, należy określić hasło hello w hello **hasło** pola.
    7. Potwierdź wprowadzone zmiany, klikając **OK**. Po nawigacji Wstecz tooyour wersji definicji, kliknij ikonę odświeżania hello na powitania **połączenia klastra** pola toosee hello punktu końcowego właśnie został dodany.
12. Zapisz hello wersji definicji.

> [!NOTE]
> Accounts firmy Microsoft (na przykład @hotmail.com lub @outlook.com) nie są obsługiwane przy użyciu uwierzytelniania usługi Azure Active Directory.
> 
> 

Definicja Hello, która jest tworzona składa się z jednego zadania typu **wdrożenia aplikacji sieci szkieletowej usług**. Zobacz hello [stronę dokumentacji zadań](https://go.microsoft.com/fwlink/?LinkId=820528) uzyskać więcej informacji dotyczących tego zadania.

### <a name="verify-hello-template-defaults"></a>Sprawdź ustawienia domyślne hello szablonu
1. Sprawdź hello **profilu publikacji** pole wejściowe dla hello **wdrażanie aplikacji sieci szkieletowej usług** zadań. Domyślnie to pole odwołuje się profil publikowania o nazwie Cloud.xml zawartych w artefakty hello kompilacji. Jeśli chcesz, aby tooreference profilu publikowania inną lub kompilacji hello zawiera wiele pakietów aplikacji w jego artefakty należy ścieżki hello tooupdate odpowiednio.
2. Sprawdź hello **pakiet aplikacji** pole wejściowe dla hello **wdrażanie aplikacji sieci szkieletowej usług** zadań. Domyślnie to pole odwołuje się do hello domyślny pakiet użyta ścieżka aplikacji hello kompilacji definicji szablonu.  Jeśli zmodyfikowano hello domyślna ścieżka pakietu aplikacji w hello definicji kompilacji, należy ścieżką hello tooupdate odpowiednio tutaj również.

### <a name="try-it"></a>Wypróbuj
Wybierz **Tworzenie wersji** z hello **wersji** przycisk menu toomanually utworzyć wersję. W oknie dialogowym hello, który zostanie otwarty, wybierz hello kompilacji, która ma toobase hello wersji na, a następnie kliknij przycisk **Utwórz**. Jeśli włączono ciągłe wdrażanie wersje zostaną utworzone automatycznie po definicji kompilacji hello skojarzone zakończeniu kompilacji.

## <a name="next-steps"></a>Następne kroki
więcej informacji na temat ciągłej integracji z aplikacjami platformy Service Fabric, przeczytaj następujące artykuły hello toolearn:

* [Dokumentacja usług Team macierzystego](https://www.visualstudio.com/docs/overview)
* [Tworzenie zarządzania w programie Team Services](https://www.visualstudio.com/docs/build/overview)
* [Zarządzania zleceniami w programie Team Services](https://www.visualstudio.com/docs/release/overview)

