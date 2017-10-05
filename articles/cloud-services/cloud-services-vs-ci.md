---
title: "Ciągłego dostarczania dla chmury usług za pomocą programu Visual Studio Online | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować ciągłego dostarczania dla aplikacji w chmurze Azure bez zapisania klucza magazynu diagnostyki w plikach konfiguracji usługi"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a>Securely Zapisz usług diagnostyki klucz magazynu w chmurze i Instalator ciągłą integrację i wdrażanie na platformie Azure przy użyciu programu Visual Studio Online
 Jest typowym rozwiązaniem do otwierania projektów źródła dzisiaj. Zapisywanie w plikach konfiguracji hasła aplikacji nie jest już bezpieczne praktyki jako luk w zabezpieczeniach są widoczne z kluczy tajnych wycieku z kontrolki źródła publicznego. Przechowywanie klucza tajnego jako zwykłego tekstu w pliku w potoku ciągłej integracji nie są chronione albo ponieważ serwery kompilacji może być udostępnionych zasobów w środowisku chmury. W tym artykule opisano, jak Visual Studio i Visual Studio Online zmniejsza kwestie zabezpieczeń podczas projektowania i proces ciągłej integracji.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Usuń hasło klucza magazynu diagnostyki w pliku konfiguracji projektu
Rozszerzenie Diagnostyka usług w chmurze wymaga magazynu Azure do zapisywania wyników diagnostyki. Wcześniej parametry połączenia magazynu jest określona w plikach konfiguracji (cscfg) usługi w chmurze i może zostać zaewidencjonowane do kontroli źródła. W najnowszej wersji zestawu Azure SDK możemy zmienić zachowanie, które będzie przechowywać parametry połączenia z częściowa tylko przy użyciu klucza zastępuje token. W poniższych krokach opisano, jak działa nowych narzędzi usługi w chmurze:

### <a name="1-open-the-role-designer"></a>1. Otwórz projektanta roli
* Kliknij dwukrotnie lub kliknij prawym przyciskiem myszy rolę usługi w chmurze, aby otworzyć projektanta roli

![Otwórz rolę projektanta][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. W sekcji Diagnostyka nowe pole wyboru "nie usuwaj magazynu klucz tajny z projektu" zostanie dodany.
* Jeśli używasz emulatora magazynu lokalnego, to pole wyboru jest wyłączone, ponieważ nie istnieje żadne klucz tajny, aby zarządzać ciągu połączenia lokalnego, który jest UseDevelopmentStorage = true.

![Parametry połączenia emulatora magazynu lokalnego nie jest tajny][1]

* W przypadku tworzenia nowego projektu, domyślnie to pole wyboru jest zaznaczone. Powoduje to sekcji klucza magazynu parametry połączenia magazynu wybranego zastępowane z tokenem. Wartość tokenu zostaną znalezione w folderze roamingu AppData bieżącego użytkownika, na przykład: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Należy pamiętać, że user\AppData folder jest kontrolowany dostęp przez logowania użytkownika i jest uznawane za bezpieczne miejsce do przechowywania kluczy tajnych programowanie.
> 
> 

![Klucz magazynu jest zapisywany w folderze profilu użytkownika][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Wybierz konto magazynu diagnostyki
* Wybierz konto magazynu, w oknie dialogowym uruchomić, klikając pozycję "..." Dodaj... Zwróć uwagę, jak parametry połączenia magazynu, które są generowane nie ma klucz konta magazynu.
* Na przykład: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)

### <a name="4----debugging-the-project"></a>4.    Debugowanie projektu
* F5, aby rozpocząć debugowania w programie Visual Studio. Wszystko, co powinny działać w taki sam sposób jak przed.
  ![Rozpocznij debugowanie lokalnie][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Opublikować projekt w programie Visual Studio
* Uruchom okno dialogowe publikowania i kontynuować logowania instrukcjami, aby opublikować applicaion na platformie Azure.

### <a name="6-additional-information"></a>6. Dodatkowe informacje
> Uwaga: Panel ustawień w Projektancie roli pozostanie, ponieważ jest on teraz. Jeśli chcesz korzystać z funkcji zarządzania tajny diagnostyki, przejdź do karty konfiguracji.
> 
> 

![Dodaj ustawienia][4]

> Uwaga: Włączenie klucza usługi Application Insights zostanie zapisana jako zwykły tekst. Klucz służy tylko do przekazywania zawartości, będzie żadnych poufnych danych na ryzyko naruszenia bezpieczeństwa.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Tworzenie i publikowanie projektu usługi w chmurze za pomocą programu Visual Studio online szablonów zadań
* Poniższe kroki pokazano, jak można skonfigurować ciągłej integracji dla projektu usługi w chmurze za pomocą programu Visual Studio online zadań:
  ### <a name="1----obtain-a-vso-account"></a>1.    Uzyskaj konto usługi VSO
* [Utwórz konto Visual Studio Online] [ Create Visual Studio Online account] Jeśli nie masz już
* [Tworzenie projektu zespołowego] [ Create team project] na koncie online programu Visual Studio

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Ustawienia kontroli wersji w programie Visual Studio
* Połącz z projektem zespołowym

![Połącz z projektem zespołowym][5]

![Wybierz projekt zespołowy do nawiązania połączenia][6]

* Dodaj projekt do kontroli źródła

![Dodaj projekt do kontroli źródła][7]

![Mapowanie projektu do folderu kontroli źródła][8]

* Sprawdź w projekcie z programu Team Explorer

![Sprawdź w projekt do kontroli źródła][9]

### <a name="3----configure-build-process"></a>3.    Konfigurowanie procesu kompilacji
* Przejdź do projektu zespołowego i dodać nowe szablony procesu kompilacji

![Dodawanie nowej kompilacji][10]

* Wybierz kompilację zadań

![Dodaj zadanie kompilacji][11]

![Wybierz szablon zadania kompilacji programu Visual Studio][12]

* Edytuj dane wejściowe zadania kompilacji. Należy dostosować parametry kompilacji w zależności od potrzeb

![Skonfiguruj zadania kompilacji][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Skonfiguruj zmienne kompilacji

![Skonfiguruj zmienne kompilacji][14]

* Dodaj zadanie, aby przekazać dane wyjściowe kompilacji

![Wybierz publikowania kompilacji listy zadań][15]

![Skonfiguruj publikowanie kompilacji listy zadań][16]

* Uruchom kompilację

![Kolejki nowej kompilacji][17]

![Wyświetl podsumowanie kompilacji][18]

* Jeśli kompilacja zakończy się pomyślnie zobaczysz wyniku podobnie jak poniżej

![Wynik kompilacji][19]

### <a name="4----configure-release-process"></a>4.    Konfigurowanie procesu publikacji
* Utwórz nową wersją

![Utwórz nową wersją][20]

* Wybierz zadanie wdrażania usługi w chmurze Azure

![Wybierz zadania wdrożenia usługi w chmurze Azure][21]

* Jak klucz konta magazynu nie zostanie zaznaczona w celu kontroli źródła, należy określić klucz tajny do ustawiania rozszerzeń diagnostyki. Rozwiń węzeł **zaawansowane opcje tworzenia nowej usługi** sekcji i edytować **klucze konta magazynu diagnostyki** parametr wejściowy. Pobiera tych danych wejściowych w wielu wierszach para klucz-wartość w formacie **[RoleName]:$(StorageAccountKey)**

> Uwaga: w przypadku konta magazynu diagnostyki w ramach tej samej subskrypcji co gdzie opublikuje aplikacji usługi w chmurze, nie trzeba wprowadzić klucz w danych wejściowych zadań wdrażania; wdrożenie programowo uzyska informacji magazynu z subskrypcji
> 
> 

![Skonfiguruj zadania wdrożenia usługi w chmurze][22]

* Użyj klucza tajnego kompilacji zmienne, aby zapisać magazynu kluczy. Do zamaskowania zmiennej jako klucza tajnego kliknij ikonę blokady po prawej stronie dane wejściowe zmiennych

![Zapisywanie magazynu kluczy w zmiennych tajny kompilacji][23]

* Tworzenie zlecenia i wdrażanie projektu na platformie Azure

![Utwórz nową wersją][24]

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej na temat ustawiania rozszerzeń diagnostyki dla usług w chmurze Azure, zobacz [Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
