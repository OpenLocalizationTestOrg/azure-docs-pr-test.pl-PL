---
title: "aaaWorking z modułów Node.js"
description: "Dowiedz się, jak toowork z modułów programu Node.js w przypadku korzystania z usługi aplikacji Azure lub usługi w chmurze."
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Using Node.js Modules with Azure applications (Używanie modułów Node.js z aplikacjami platformy Azure)
Ten dokument zawiera wskazówki dotyczące używania modułów Node.js z aplikacjami hostowanej na platformie Azure. Zwraca uwagę na upewnienie się, że aplikacja korzysta z odpowiedniej wersji modułu, a także opisuje korzystanie z modułów natywnych w systemie Azure.

Jeśli znasz już przy użyciu modułów Node.js **package.json** i **npm shrinkwrap.json** pliki, hello następujących informacji zawiera podsumowanie szybkie co opisano w tym artykule:

* Rozumie, usługa aplikacji Azure **package.json** i **npm shrinkwrap.json** pliki i można zainstalować na podstawie pozycji w tych plikach modułów.

* Usługi w chmurze Azure oczekiwać wszystkich toobe modułów zainstalowanych na powitania Środowisko deweloperskie i hello **węzła\_modułów** dołączone jako część pakietu wdrożeniowego hello toobe katalogu. Jest możliwe tooenable Obsługa instalowania modułów za pomocą **package.json** lub **npm shrinkwrap.json** plików na usługi w chmurze; ta konfiguracja wymaga jednak dostosowywania domyślnego hello skryptów używanych przez projekty usługi w chmurze. Na przykład jak tooconfigure tego środowiska, zobacz [Azure uruchamiania zadań toorun npm zainstalować tooavoid Wdrażanie modułów węzła](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> Maszyny wirtualne platformy Azure nie omówiono w tym artykule jako środowisko wdrażania hello na maszynie wirtualnej jest zależny od systemu operacyjnego hello obsługiwanych przez hello maszyny wirtualnej.
> 
> 

## <a name="nodejs-modules"></a>Moduły środowiska node.js
Moduły są obciążana pakiety języka JavaScript, które zapewniają określonych funkcji aplikacji. Moduły zwykle są instalowane za pomocą hello **npm** wiersza polecenia narzędzia, jednak niektóre moduły (takich jak moduł http hello) są dostarczane jako część pakietu środowiska Node.js hello core.

Po zainstalowaniu moduły są przechowywane w hello **węzła\_modułów** katalogu głównego hello struktury katalogu aplikacji. Każdego modułu w ramach hello **węzła\_modułów** directory zachowuje własną **węzła\_modułów** katalog, który zawiera wszystkie moduły zależy, które powtarza to zachowanie dla każdego modułu końca hello dół hello łańcuch zależności. To środowisko umożliwia każdej toohave zainstalowany moduł własną wersję wymagania dotyczące modułów hello zależy, jednak może to spowodować bardzo dużych strukturą katalogów.

Wdrażanie hello **węzła\_modułów** katalogu jako części aplikacji pozwala zwiększyć rozmiar hello hello wdrożenia w porównaniu toousing **package.json** lub  **npm shrinkwrap.json** pliku; jednak gwarantuje, że wersje hello moduły hello używane w środowisku produkcyjnym są takie same hello jako moduły hello używane do rozwoju.

### <a name="native-modules"></a>Moduły macierzyste
Większość modułów są pliki JavaScript po prostu zwykłego tekstu, niektóre moduły są obrazy binarne specyficzne dla platformy. Te moduły są kompilowane w czasie instalacji, zwykle za pomocą języka Python i gyp węzła. Ponieważ usługi w chmurze Azure polegać na powitania **węzła\_modułów** folderu wdrażany w ramach aplikacji hello, każdy moduł macierzysty będących częścią hello zainstalowane moduły powinny działać w usłudze w chmurze tak długo, jak było zainstalowane i skompilowane również w rozwoju systemu Windows.

Usługa aplikacji Azure nie obsługuje wszystkie moduły natywne i może zakończyć się niepowodzeniem w przypadku kompilowania kodu modułów z określonych wymagań wstępnych. Niektóre popularnych modułów, takich jak bazy danych MongoDB opcjonalne zależnościami macierzystego i działają prawidłowo bez obawy, dwa obejścia potwierdza, że pomyślnie z prawie wszystkie moduły macierzyste dostępne dzisiaj:

* Uruchom **instalacji narzędzia npm** na komputerze z systemem Windows, który ma zainstalowane wymagania wstępne wszystkich hello modułu macierzystego w. Następnie Wdróż hello utworzony **węzła\_modułów** folder jako część tooAzure aplikacji hello usługi aplikacji.

  * Przed skompilowaniem, sprawdź, czy lokalnej instalacji programu Node.js ma architekturę zgodną i wersja hello jest możliwie możliwe toohello, używany w Azure (bieżące wartości hello można sprawdzić na środowisko uruchomieniowe przy użyciu właściwości **process.arch**i **process.version**).

* Usługa aplikacji Azure mogą być bash niestandardowych skonfigurowanych tooexecute lub skryptów powłoki podczas wdrażania, umożliwiając hello polecenia niestandardowych tooexecute możliwości i dokładnie skonfigurować hello sposób **instalacji narzędzia npm** jest uruchamiana. Dla wideo przedstawiający sposób tooconfigure tego środowiska, zobacz [niestandardowych skryptów wdrażania witryny sieci Web z Kudu].

### <a name="using-a-packagejson-file"></a>Przy użyciu pliku package.json
Witaj **package.json** plik jest sposób toospecify hello najwyższego poziomu zależności aplikacja wymaga, aby hello Platforma macierzysta można zainstalować zależności hello zamiast konieczności tooinclude hello **węzła \_pakiety** folder jako część wdrożenia hello. Po wdrożeniu aplikacji hello hello **instalacji narzędzia npm** hello tooparse używane jest polecenie **package.json** plików i zainstalować wszystkie zależności hello na liście.

Podczas tworzenia, można użyć hello **— Zapisz**, **— Zapisz deweloperów**, lub **— opcjonalnie Zapisz** parametrów podczas instalowania modułów tooadd wpis dotyczący hello modułu tooyour **package.json** pliku automatycznie. Aby uzyskać więcej informacji, zobacz [npm install](https://docs.npmjs.com/cli/install).

Jeden potencjalny problem z hello **package.json** plik jest, że tylko określa wersję hello zależności najwyższego poziomu. Każdego zainstalowany moduł może lub nie mógł określić wersji hello modułów hello, od których zależy, a więc jest to możliwe, że może to spowodować z łańcucha zależności innego niż hello używany w rozwoju.

> [!NOTE]
> W przypadku wdrażania tooAzure usługi aplikacji, jeśli Twoje <b>package.json</b> odwołuje się do pliku modułu macierzystego można napotkać błąd toohello podobnie poniższy przykład w przypadku publikowania aplikacji hello przy użyciu narzędzia Git:
> 
> Błąd npm! module-name@0.6.0Zainstaluj: "gyp węzła Konfigurowanie kompilacji"
> 
> Błąd npm! "cmd"/ c""gyp węzła Konfigurowanie kompilacji"" nie powiodło się z 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>Przy użyciu pliku npm shrinkwrap.json
Witaj **npm shrinkwrap.json** plik jest próba tooaddress hello modułu versioning ograniczenia hello **package.json** pliku. Podczas hello **package.json** plik zawiera tylko wersje hello moduły najwyższego poziomu, hello **npm shrinkwrap.json** plik zawiera hello wersji wymagania dotyczące łańcuch zależności hello pełne modułu.

Gdy aplikacja jest gotowa do produkcji, można zablokować wymagania dotyczące wersji i utworzyć **npm shrinkwrap.json** pliku przy użyciu hello **npm shrinkwrap** polecenia. Tego polecenia będą używać wersji hello aktualnie zainstalowane w hello **węzła\_modułów** folderu i Zapisz te wersje toohello **npm shrinkwrap.json** pliku. Po aplikacji hello został wdrożony toohello Środowisko hostingu, hello **instalacji narzędzia npm** hello tooparse używane jest polecenie **npm shrinkwrap.json** plików i zainstalować wszystkie zależności hello na liście. Aby uzyskać więcej informacji, zobacz [npm shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

> [!NOTE]
> W przypadku wdrażania tooAzure usługi aplikacji, jeśli Twoje <b>npm shrinkwrap.json</b> odwołuje się do pliku modułu macierzystego można napotkać błąd toohello podobnie poniższy przykład w przypadku publikowania aplikacji hello przy użyciu narzędzia Git:
> 
> Błąd npm! module-name@0.6.0Zainstaluj: "gyp węzła Konfigurowanie kompilacji"
> 
> Błąd npm! "cmd"/ c""gyp węzła Konfigurowanie kompilacji"" nie powiodło się z 1
> 
> 

## <a name="next-steps"></a>Następne kroki
Zapoznaniu się jak toouse modułów Node.js z platformy Azure, Dowiedz się, jak za[określanie wersji środowiska Node.js hello], [tworzenia i wdrażania aplikacji sieci web Node.js](app-service-web/app-service-web-get-started-nodejs.md), i [jak toouse hello Azure wiersza polecenia Interfejs dla komputerów Mac i Linux].

Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów środowiska Node.js](/nodejs/azure/).

[określanie wersji środowiska Node.js hello]: nodejs-specify-node-version-azure-apps.md
[jak toouse hello Azure wiersza polecenia Interfejs dla komputerów Mac i Linux]:cli-install-nodejs.md
[niestandardowych skryptów wdrażania witryny sieci Web z Kudu]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
