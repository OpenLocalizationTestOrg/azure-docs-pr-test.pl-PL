---
title: aaaLog w tooAzure z hello interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
description: "Połącz tooyour subskrypcji platformy Azure z hello interfejsu wiersza polecenia platformy Azure (Azure CLI) dla komputerów Mac, Linux i Windows"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>Zaloguj się za tooAzure z hello wiersza polecenia platformy Azure
Hello Azure CLI jest zestaw poleceń open source, obsługujący wiele platform do pracy z zasobów platformy Azure. W tym artykule opisano tooprovide różne sposoby hello konta Azure poświadczenia tooconnect hello Azure CLI tooyour subskrypcji platformy Azure:

* Uruchom hello `azure login` tooauthenticate polecenia interfejsu wiersza polecenia za pomocą usługi Azure Active Directory. To zapewnia metody dostęp polecenia tooCLI zarówno [polecenia tryby](#cli-command-modes). Po uruchomieniu polecenia hello bez dodatkowych opcji `azure login` monit toocontinue interakcyjnie zalogować się za pośrednictwem portalu sieci web. Aby uzyskać dodatkowe `azure login` polecenia opcji, zobacz hello scenariusze w tym artykule, lub typ `azure login --help`.
* Jeśli wymagane jest tylko toouse zarządzania usługą Azure CLI polecenia w trybie (nie zalecane dla większości nowych wdrożeń), można pobrać i zainstalować plik ustawień publikowania na tym komputerze.

Jeśli nie została jeszcze zainstalowana hello interfejsu wiersza polecenia, zobacz [hello instalowanie interfejsu wiersza polecenia Azure](cli-install-nodejs.md). Jeśli nie masz subskrypcji Azure, możesz utworzyć [bezpłatne konto](http://azure.microsoft.com/free/) w zaledwie kilka minut.

Aby uzyskać ogólne informacje o tożsamości z innego konta i subskrypcji platformy Azure, zobacz [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="scenario-1-azure-login-with-interactive-login"></a>Scenariusz 1: azure logowania przy użyciu logowania interakcyjnego
Z określonymi kontami hello interfejsu wiersza polecenia wymaga toorun `azure login` , a następnie kontynuuj hello proces logowania przy użyciu przeglądarki sieci web za pośrednictwem portalu sieci web, w procesie nazywanym *logowania interakcyjnego*. Typową przyczyną jest, jeśli masz konto służbowe (nazywane również *konta organizacyjnego*) skonfigurowane uwierzytelnianie wieloskładnikowe toorequire. Za pomocą logowania interaktywnego Twojego konta Microsoft, należy toouse polecenia w trybie Menedżera zasobów.

Interakcyjne logowanie jest łatwe: typ `azure login` — bez żadnych opcji--pokazane na powitania poniższy przykład:

```
azure login
```                                                                                             

zostaną wyświetlone dane wyjściowe Hello, przypominać następujące hello:

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
Skopiuj kod hello oferowane tooyou w danych wyjściowych polecenia hello i otworzyć toohttp://aka.ms/devicelogin przeglądarki lub inne strony, jeśli określony. (Można otworzyć przeglądarki na powitania tym samym komputerze lub na innym komputerze lub urządzeniu.) Wprowadź kod hello, a następnie są tooenter zostanie wyświetlony monit o hello użytkownika i hasło dla tożsamości hello ma toouse. Po zakończeniu tego procesu powłoki poleceń hello kończy hello logowania. Może wyglądać mniej więcej tak:

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> Z logowania interakcyjnego uwierzytelnianie i autoryzacja są wykonywane przy użyciu usługi Azure Active Directory. Jeśli używasz tożsamość konta Microsoft, procesu logowania hello uzyskuje dostęp do domeny domyślnej usługi Azure Active Directory. (Jeśli zostało zarejestrowane w bezpłatne konto platformy Azure, Azure Active Directory tworzone domyślną domenę dla konta.)
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>Scenariusz 2: azure Zaloguj się za pomocą nazwy użytkownika i hasła
Użyj hello `azure login` polecenia hello username (`-u`) tooauthenticate parametru toouse służbowy lub konto służbowe, które nie wymaga uwierzytelniania wieloskładnikowego. Zostanie wyświetlony monit, w wierszu polecenia hello hello hasła (lub hasło hello można przekazać opcjonalnie jako dodatkowy parametr hello `azure login` polecenia). Witaj w poniższym przykładzie przekazuje hello nazwę użytkownika konta organizacji:

    azure login -u myUserName@contoso.onmicrosoft.com

Będzie monitowany tooenter hasło:

    info:    Executing command login
    Password: *********

następnie kończy proces logowania Hello.

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

Jeśli jest to Twoje pierwsze rejestrowania w czasie przy użyciu tych poświadczeń, zostanie wyświetlona prośba tooverify ma toocache tokenu uwierzytelniania. Ten monit występuje także jeśli poprzednio korzystano hello `azure logout` polecenia (opisane w dalszej części artykułu hello). Uruchom ten wiersz w scenariuszach automatyzacji toobypass `azure login` z hello `-q` parametru.

## <a name="scenario-3-azure-login-with-a-service-principal"></a>Scenariusz 3: azure logowania przy użyciu nazwy głównej usługi
Jeśli tworzenie nazwy głównej usługi dla aplikacji usługi Active Directory, a hello nazwy głównej usługi ma uprawnienia do subskrypcji, możesz użyć hello `azure login` polecenia tooauthenticate hello service principal. W zależności od scenariusza, można podać poświadczenia hello głównej usługi hello jako jawne parametry hello `azure login` polecenia. Na przykład hello następujące polecenie przekazuje hello główną nazwę usługi i identyfikator dzierżawy usługi Active Directory:

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

Jesteś, a następnie zostanie wyświetlony monit o tooprovide hello hasła. Można również podać poświadczenia hello za pośrednictwem interfejsu wiersza polecenia kodu skryptu lub aplikacji lub nieinteraktywnie Użyj nazwy głównej usługi hello tooauthenticate certyfikatów w scenariuszach automatyzacji. Aby uzyskać szczegółowe informacje i przykłady, zobacz [uwierzytelniania nazwy głównej usługi z usługą Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).

## <a name="scenario-4-use-a-publish-settings-file"></a>Scenariusz 4: Korzystanie z pliku ustawień publikowania
Jeśli wymagane jest tylko toouse hello zarządzania usługą Azure tryb polecenia interfejsu wiersza polecenia (na przykład toodeploy maszynach wirtualnych platformy Azure w hello klasycznego modelu wdrażania), możesz połączyć za pomocą pliku ustawień publikowania. Ta metoda instaluje certyfikat na komputerze lokalnym, który umożliwia tooperform zadania zarządzania dla tak długo, jak hello subskrypcji i certyfikatu hello są prawidłowe.

* **Plik ustawień publikowania toodownload hello** Twojego konta, upewnij się, że hello interfejsu wiersza polecenia jest w trybie zarządzania usługami, wpisując `azure config mode asm`. Następnie uruchom następujące polecenie hello:

        azure account download

To uruchomi domyślną przeglądarkę i wyświetli monit o toosign w toohello [klasycznego portalu Azure](https://manage.windowsazure.com). Po zalogowaniu, `.publishsettings` pliku pliki do pobrania. Zanotuj miejsce, w którym plik został zapisany.

> [!NOTE]
> Jeśli Twoje konto jest skojarzone z wieloma dzierżawcami usługi Azure Active Directory, może być zostanie wyświetlony monit o tooselect, które usługi Active Directory mają toodownload ustawień publikowania plików do.
>
>

Po wybraniu za pomocą strony pobierania hello lub poprzez odwiedzenie hello klasycznego portalu Azure, hello wybranej usługi Active Directory staje się hello domyślne używane przez hello klasyczny portal i strony pobierania. Po ustanowieniu domyślny, zostanie wyświetlony tekst hello "**kliknij tutaj, strona wyboru toohello tooreturn**" u góry hello hello pobierania strony. Użyj hello podane łącze tooreturn toohello wybór strony.

* **Plik ustawień publikowania tooimport hello**Uruchom hello następujące polecenie:

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> Po zaimportowaniu Twoje ustawienia publikowania, należy usunąć hello `.publishsettings` pliku. Nie jest już wymagana przez hello wiersza polecenia platformy Azure, a stanowi zagrożenie bezpieczeństwa, ponieważ może być używane toogain dostępu tooyour subskrypcji.
>
>

## <a name="cli-command-modes"></a>Tryby polecenia interfejsu wiersza polecenia
Hello Azure CLI dostępne są dwa tryby polecenia do pracy z zasobami Azure z zestawami inne polecenie:

* **Tryb usługi Resource Manager** — w przypadku pracy z zasobami platformy Azure w modelu wdrażania usługi Resource Manager hello. tooset ten tryb, uruchom `azure config mode arm`.
* **Tryb zarządzania usługami** — w przypadku pracy z zasobami platformy Azure w hello klasycznego modelu wdrażania. tooset ten tryb, uruchom `azure config mode asm`.

Podczas pierwszej instalacji hello bieżącej wersji powitalne interfejsu wiersza polecenia jest w trybie Menedżera zasobów.

> [!NOTE]
> tryb usługi Resource Manager Hello i tryb usługi zarządzania wzajemnie się wykluczają. Oznacza to, że nie mogą być zarządzane zasoby utworzone w trybie jednego z hello innych tryb.
>
>

## <a name="multiple-subscriptions"></a>Wiele subskrypcji
Jeśli masz wiele subskrypcji Azure, łączenie tooAzure udziela dostępu tooall subskrypcji skojarzonych z poświadczeń. Jedna subskrypcja jest wybrana jako domyślna hello i używane przez hello interfejsu wiersza polecenia Azure podczas wykonywania operacji. Można wyświetlić hello subskrypcji, włącznie z bieżącej subskrypcji domyślne hello, przy użyciu hello `azure account list` polecenia. To polecenie zwraca informacje o podobnych toohello poniżej:

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

W powyższej listy hello, hello **bieżącego** kolumna wskazuje domyślną hello subskrypcję Azure-sub-1. toochange hello domyślne subskrypcji, użyj hello `azure account set` polecenia, a następnie określ hello subskrypcji, że chcesz toobe hello domyślne. Na przykład:

    azure account set Azure-sub-2

Spowoduje to zmianę hello domyślne subskrypcji tooAzure-sub-2.

> [!NOTE]
> Zmiana hello Domyślna subskrypcja ma efekt natychmiastowy i zmiana globalnych; nowe polecenia interfejsu wiersza polecenia Azure, czy uruchamiać je z hello sam wiersza polecenia lub innej wystąpieniu, użyj hello nową subskrypcję domyślne.
>
>

Jeśli chcesz toouse subskrypcji innych niż domyślne z hello wiersza polecenia platformy Azure, ale nie mają toochange hello bieżące domyślne, możesz użyć hello `--subscription` opcji dla polecenia hello i podaj nazwę hello hello subskrypcji chcesz toouse hello operacji.

Gdy są połączone tooyour subskrypcji platformy Azure, możesz rozpocząć używać toowork polecenia interfejsu wiersza polecenia Azure hello z zasobów platformy Azure.

## <a name="storage-of-cli-settings"></a>Magazyn ustawień interfejsu wiersza polecenia
Określa, czy możesz zalogować się hello `azure login` polecenia lub importowania ustawień publikowania, profilu interfejsu wiersza polecenia i dzienniki są przechowywane w `.azure` katalog znajduje się w sieci `user` katalogu. Twoje `user` katalogu jest chroniony przez system operacyjny. Jednak zaleca się wykonanie dodatkowych kroków tooencrypt Twojego `user` katalogu. Możesz to zrobić w hello następujące sposoby:

* W systemie Windows zmodyfikuj właściwości directory hello, lub użyj funkcji BitLocker.
* Dla komputerów Mac należy włączyć funkcję FileVault hello katalogu.
* Na Ubuntu funkcja hello zaszyfrowane głównej katalogu. Inne dystrybucje systemu Linux oferuje podobne funkcje.

## <a name="logging-out"></a>Wylogowywanie
toolog limit hello Użyj następującego polecenia:

    azure logout -u <username>

Jeśli hello subskrypcji skojarzonych z konta hello tylko są uwierzytelniane z usługą Active Directory, rejestrowanie usuwa hello subskrypcji informacje z profilu lokalne powitania. Jednak także zaimportowano plik ustawień publikowania dla subskrypcji hello, rejestrowanie tylko informacje z profilu lokalne powitania związane z usuwa usługi Active Directory.

## <a name="next-steps"></a>Następne kroki
* toouse poleceń interfejsu wiersza polecenia Azure, zobacz [polecenia wiersza polecenia platformy Azure w trybie Menedżera zasobów](virtual-machines/azure-cli-arm-commands.md) i [polecenia wiersza polecenia platformy Azure w trybie zarządzania usługami](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* toolearn więcej informacji na temat hello Azure CLI, pobrać kodu źródłowego, zgłaszanie problemów, lub współtworzenia toohello projektu, odwiedź hello [repozytorium GitHub hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* Jeśli wystąpią problemy przy użyciu hello Azure CLI lub Azure, odwiedź hello [fora Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).
