---
title: "dostarczanie aaaContinuous chmury usług za pomocą programu Visual Studio Online | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset się ciągłego dostarczania dla platformy Azure aplikacji w chmurze bez zapisywania plików konfiguracyjnych usługi toohello klucza magazynu diagnostyki"
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
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely Zapisz usług diagnostyki klucz magazynu w chmurze i tooAzure Instalatora ciągłej integracji i wdrażania przy użyciu programu Visual Studio Online
 Wspólne projekty źródła tooopen rozwiązaniem jest obecnie. Zapisywanie w plikach konfiguracji hasła aplikacji nie jest już bezpieczne praktyki jako luk w zabezpieczeniach są widoczne z kluczy tajnych wycieku z kontrolki źródła publicznego. Przechowywanie klucza tajnego jako zwykłego tekstu w pliku w potoku ciągłej integracji nie są chronione albo ponieważ serwery kompilacji może być udostępnionych zasobów w środowisku chmury hello. W tym artykule opisano, jak Visual Studio i Visual Studio Online zmniejsza hello bezpieczeństwo podczas procesu ciągłej integracji i rozwoju.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Usuń hasło klucza magazynu diagnostyki w pliku konfiguracji projektu
Rozszerzenie Diagnostyka usług w chmurze wymaga magazynu Azure do zapisywania wyników diagnostyki. Wcześniej parametry połączenia magazynu hello jest określona w plikach konfiguracji (cscfg) hello usługi w chmurze i można sprawdzić w formancie toosource. W najnowszej wersji zestawu Azure SDK hello możemy zmienić magazynu tooonly zachowanie hello parametrów połączenia częściowe kluczem hello zastępuje token. Hello następujące kroki opisano, jak działa hello nowych narzędzi usługi w chmurze:

### <a name="1-open-hello-role-designer"></a>1. Otwórz projektanta roli hello
* Kliknij dwukrotnie lub kliknij prawym przyciskiem myszy Projektanta roli tooopen roli usługi w chmurze

![Otwórz rolę projektanta][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. W sekcji Diagnostyka nowe pole wyboru "nie usuwaj magazynu klucz tajny z projektu" zostanie dodany.
* Jeśli używasz emulatora magazynu lokalne powitania to pole wyboru jest wyłączona, ponieważ nie istnieje żadne tajny toomanage dla parametrów połączenia lokalne powitania, czyli UseDevelopmentStorage = true.

![Parametry połączenia emulatora magazynu lokalnego nie jest tajny][1]

* W przypadku tworzenia nowego projektu, domyślnie to pole wyboru jest zaznaczone. Powoduje to hello magazynu kluczy części parametrów połączenia magazynu hello wybrane zastępowane z tokenem. Witaj wartość tokenu hello zostaną znalezione w folderze roamingu AppData hello bieżącego użytkownika, na przykład: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Należy pamiętać, ten folder user\AppData hello jest kontrolowany dostęp przez logowania użytkownika i jest uznawany za kluczy tajnych programowanie dla toostore w bezpiecznym miejscu.
> 
> 

![Klucz magazynu jest zapisywany w folderze profilu użytkownika][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Wybierz konto magazynu diagnostyki
* Wybierz konto magazynu z okna dialogowego hello uruchomić, klikając pozycję "..." hello Dodaj... Zwróć uwagę, jak parametry połączenia magazynu hello wygenerowany nie będzie miał klucz konta magazynu hello.
* Na przykład: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.    Debugowanie projektu hello
* Toostart F5 debugowania w programie Visual Studio. Wszystko, co powinny działać w hello sam sposób jak wcześniej.
  ![Rozpocznij debugowanie lokalnie][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Opublikować projekt w programie Visual Studio
* Uruchom hello okna dialogowego publikowania i kontynuować logowania instrukcje toopublish hello applicaion tooAzure.

### <a name="6-additional-information"></a>6. Dodatkowe informacje
> Uwaga: hello panel ustawień w Projektancie roli hello pozostanie, ponieważ jest on obecnie. Funkcja zarządzania tajny hello toouse diagnostyki, przejdź toohello konfiguracji karty.
> 
> 

![Dodaj ustawienia][4]

> Uwaga: Włączenie klucza usługi Application Insights hello będą przechowywane jako zwykły tekst. klucz Hello jest używana tylko do przekazywania zawartości tak będzie żadnych poufnych danych na ryzyko naruszenia bezpieczeństwa.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Tworzenie i publikowanie projektu usługi w chmurze za pomocą programu Visual Studio online szablonów zadań
* Hello następujące kroki przedstawiono sposób toosetup ciągłej integracji usług w chmurze projektu za pomocą programu Visual Studio online zadań:
  ### <a name="1----obtain-a-vso-account"></a>1.    Uzyskaj konto usługi VSO
* [Utwórz konto Visual Studio Online] [ Create Visual Studio Online account] Jeśli nie masz już
* [Tworzenie projektu zespołowego] [ Create team project] na koncie online programu Visual Studio

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Ustawienia kontroli wersji w programie Visual Studio
* Połącz tooa projektu zespołowego

![Łączenie tooteam projektu][5]

![Wybierz tooconnect projektu zespołowego do][6]

* Dodawanie formantu toosource projektu

![Dodawanie formantu toosource projektu][7]

![Mapowania folderu kontroli źródła tooa projektu][8]

* Sprawdź w projekcie z programu Team Explorer

![Sprawdź w formancie toosource projektu][9]

### <a name="3----configure-build-process"></a>3.    Konfigurowanie procesu kompilacji
* Przeglądanie projektu zespołowego tooyour i dodać nowe szablony procesu kompilacji

![Dodawanie nowej kompilacji][10]

* Wybierz kompilację zadań

![Dodaj zadanie kompilacji][11]

![Wybierz szablon zadania kompilacji programu Visual Studio][12]

* Edytuj dane wejściowe zadania kompilacji. Należy dostosować parametry zgodnie z tooyour wymagają kompilacji hello

![Skonfiguruj zadania kompilacji][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Skonfiguruj zmienne kompilacji

![Skonfiguruj zmienne kompilacji][14]

* Dodaj dane wyjściowe kompilacji tooupload zadań

![Wybierz publikowania kompilacji listy zadań][15]

![Skonfiguruj publikowanie kompilacji listy zadań][16]

* Uruchom hello kompilacji

![Kolejki nowej kompilacji][17]

![Wyświetl podsumowanie kompilacji][18]

* Jeśli hello kompilacja zakończy się pomyślnie zobaczysz toobelow podobne wyników

![Wynik kompilacji][19]

### <a name="4----configure-release-process"></a>4.    Konfigurowanie procesu publikacji
* Utwórz nową wersją

![Utwórz nową wersją][20]

* Wybierz zadanie wdrażania usługi w chmurze Azure hello

![Wybierz zadania wdrożenia usługi w chmurze Azure][21]

* Ponieważ klucz konta magazynu hello nie jest zaznaczona w formancie toosource, potrzebujemy klucz tajny hello toospecify do ustawiania rozszerzeń diagnostyki. Rozwiń węzeł hello **zaawansowane opcje tworzenia nowej usługi** sekcji i edytować hello **klucze konta magazynu diagnostyki** parametr wejściowy. Pobiera tych danych wejściowych w wielu wierszach para klucz-wartość w formacie hello **[RoleName]:$(StorageAccountKey)**

> Uwaga: Jeśli diagnostycznej konto magazynu znajduje się w obszarze hello tej samej subskrypcji co którym będą publikowane hello aplikacji usługi w chmurze, nie ma klucza hello tooenter w danych wejściowych zadań wdrażania hello; wdrożenie Hello programowo uzyska hello magazynu informacji z subskrypcji
> 
> 

![Skonfiguruj zadania wdrożenia usługi w chmurze][22]

* Użyj klucza tajnego kompilacji toosave zmienne magazynu kluczy. toomask zmiennej jako klucza tajnego kliknij ikonę blokady powitania po prawej stronie powitania hello zmienne wejściowe

![Zapisywanie magazynu kluczy w zmiennych tajny kompilacji][23]

* Tworzenie zlecenia i wdrażanie tooAzure Twojego projektu

![Utwórz nową wersją][24]

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat ustawiania rozszerzeń diagnostyki dla usług w chmurze Azure, zobacz [Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]

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
