---
title: "Omówienie aplikacji usługi lokalnej pamięci podręcznej aaaAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooenable, zmiany rozmiaru i zapytania hello stan hello funkcji lokalnej pamięci podręcznej Azure App Service"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Omówienie usługi Azure App Service lokalnej pamięci podręcznej
Zawartość aplikacji sieci web platformy Azure są przechowywane w magazynie Azure i jest udostępniane w górę w sposób trwały jako udział zawartości. Ten projekt jest zamierzone toowork z różnych aplikacji i ma hello następujące atrybuty:  

* zawartość Hello jest współużytkowany przez wielu wystąpień maszyny wirtualnej (VM) hello aplikacji sieci web.
* zawartość Hello są trwałe i mogą być modyfikowane przez uruchamianie aplikacji sieci web.
* Plików dziennika i plików danych diagnostycznych są dostępne w obszarze hello sam zawartości folderu udostępnionego.
* Publikowanie nowej zawartości bezpośrednio aktualizacje hello folder zawartości. Możesz natychmiast hello widoku sam zawartości za pośrednictwem witryny sieci Web hello SCM i hello uruchomionej aplikacji sieci web (zwykle niektórych technologii, takich jak ASP.NET zainicjować ponowne uruchomienie aplikacji sieci web na niektóre zmiany tooget hello najnowszej zawartości pliku).

Podczas gdy wiele aplikacji sieci web co najmniej jedną z tych funkcji, niektóre aplikacje sieci web, wystarczy wysokiej wydajności, tylko do odczytu magazynu zawartości, które mogą uruchamiać z o wysokiej dostępności. Te aplikacje mogą korzystać z maszyny Wirtualnej wystąpienie określonego lokalnej pamięci podręcznej.

Witaj lokalnej pamięci podręcznej Azure App Service udostępnia widok roli sieci web zawartości. Ta zawartość jest pamięć podręczną zapisu — ale odrzucenia zawartości magazynu, które utworzono asynchronicznie podczas uruchamiania witryny. Gdy hello pamięci podręcznej jest gotowy, lokacji hello jest wyłączone toorun hello w pamięci podręcznej zawartości. Aplikacje sieci Web, które działają w lokalnej pamięci podręcznej mają hello następujące korzyści:

* Są one odporna toolatencies, które występują przy uzyskiwaniu dostępu do zawartości w magazynie Azure.
* Są one uaktualnień odporna toohello planowane lub nieplanowane przestoje powodowane przez oraz innych zakłóceń z usługą Azure Storage, występujących na serwerach obsługujących hello udziału zawartości.
* Mają one mniej uruchomieniu aplikacji zmiany udziału toostorage ukończenia.

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>Jak lokalnej pamięci podręcznej zmienia zachowanie hello usługi App Service
* Witaj lokalnej pamięci podręcznej jest kopią hello /site i /siteextensions folderów hello aplikacji sieci web. Jest tworzona na powitania lokalne wystąpienie maszyny Wirtualnej podczas uruchamiania aplikacji sieci web. Witaj rozmiar hello lokalnej pamięci podręcznej dla aplikacji sieci web jest ograniczony MB too300 przez domyślny, ale może zwiększyć jej zapasowej too2 GB.
* Witaj lokalnej pamięci podręcznej jest do odczytu / zapisu. Jednak wszelkie modyfikacje zostaną odrzucone po maszyny wirtualne są przenoszone lub pobiera ponownego uruchomienia aplikacji sieci web hello. Dla aplikacji przechowujących kluczowych danych w magazynie zawartości hello nie należy używać lokalnej pamięci podręcznej.
* Aplikacje sieci Web można nadal toowrite pliki dzienników i danych diagnostycznych, tak jak obecnie. Pliki dzienników i danych, jednak są przechowywane lokalnie na powitania maszyny Wirtualnej. Następnie są one kopiowane za pośrednictwem okresowo toohello magazynu zawartości udostępnionej. Witaj magazynu zawartości udostępnionej toohello kopiowania jest najlepszym nakładu — tworzy kopię zapisu mogą zostać utracone powodu tooa nagła awaria wystąpienia maszyny Wirtualnej.
* Brak zmian w strukturze folderu hello hello LogFiles i folderów danych aplikacji sieci web, które używają lokalnej pamięci podręcznej. Istnieją teraz podfoldery w hello magazynu LogFiles danych folderów i przestrzeganie hello wzorzec nazewnictwa "Unikatowy identyfikator" + sygnatury czasowej. Każdy z podfolderów hello odpowiada tooa wystąpienia maszyny Wirtualnej, której hello aplikacji sieci web jest uruchomiona lub jest uruchomione.  
* Publikowanie aplikacji sieci web za pomocą tych mechanizmów publikowania hello zmiany toohello będą publikować toohello magazynu zawartości udostępnionej. To jest celowe, ponieważ chcemy hello opublikowany zawartości toobe trwałe. toorefresh hello lokalnej pamięci podręcznej hello aplikacji sieci web, musi on toobe ponownego uruchomienia. To wydawać nadmiernego krok? toomake hello cyklu życia bezproblemowe, zobacz informacje hello w dalszej części tego artykułu.
* D:\Home wskaże toohello lokalnej pamięci podręcznej. D:\Local będzie wskazanie tymczasowego magazynu określonych toohello maszyny Wirtualnej.
* Widok zawartości domyślny Hello hello SCM lokacji będą nadal toobe, który hello udostępniony magazyn zawartości.

## <a name="enable-local-cache-in-app-service"></a>Włącz lokalnej pamięci podręcznej w usłudze App Service
Konfigurowanie lokalnej pamięci podręcznej przy użyciu kombinacji ustawień aplikacji zastrzeżone. Te ustawienia aplikacji można skonfigurować za pomocą hello następujące metody:

* [Witryna Azure Portal](#Configure-Local-Cache-Portal)
* [Azure Resource Manager](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>Skonfiguruj lokalnej pamięci podręcznej za pomocą hello portalu Azure
<a name="Configure-Local-Cache-Portal"></a>

Można włączyć lokalnej pamięci podręcznej na podstawie dla sieci web aplikacji za pomocą tego ustawienia aplikacji:`WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Ustawienia aplikacji portalu Azure: lokalnej pamięci podręcznej](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>Skonfiguruj lokalnej pamięci podręcznej za pomocą usługi Azure Resource Manager
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>Zmień ustawienie rozmiaru hello w lokalnej pamięci podręcznej
Domyślny rozmiar pamięci podręcznej lokalne powitania to **300 MB**. Obejmuje to hello /site i /siteextensions folderów, które są kopiowane z hello zawartości, Magazyn, jak również żadnego lokalnie tworzone foldery dzienników i danych. tooincrease to ograniczenie, użyj ustawienia aplikacji hello `WEBSITE_LOCAL_CACHE_SIZEINMB`. Można zwiększyć rozmiar hello Konfigurowanie zbyt**2 GB** (2000 MB) dla aplikacji sieci web.

## <a name="best-practices-for-using-app-service-local-cache"></a>Najlepsze rozwiązania dotyczące korzystania z lokalnej pamięci podręcznej usługi aplikacji
Zalecane jest użycie lokalnej pamięci podręcznej w połączeniu z hello [środowiska przejściowe](../app-service-web/web-sites-staged-publishing.md) funkcji.

* Dodaj hello *trwałe* ustawienie aplikacji `WEBSITE_LOCAL_CACHE_OPTION` z wartością hello `Always` tooyour **produkcji** miejsca. Jeśli używasz `WEBSITE_LOCAL_CACHE_SIZEINMB`, dodaj go jako gnieździe produkcyjnym tooyour ustawienie trwałe.
* Utwórz **przemieszczania** gniazdo i opublikuj gnieździe przemieszczania tooyour. Zazwyczaj nie zostanie ustawiona hello przemieszczania toouse miejsca w lokalnej pamięci podręcznej tooenable bezproblemowe cykl kompilacja wdrażanie testy dla przemieszczania, jeśli do miejsca produkcji hello hello korzyści z lokalnej pamięci podręcznej.
* Testowanie witryny Twojego miejsca przemieszczania.  
* Gdy wszystko będzie gotowe do wydania [operacji wymiana](../app-service-web/web-sites-staged-publishing.md#Swap) między przemieszczania i produkcji gniazd.  
* Trwałe ustawienia zawierają nazwę i miejsce tooa trwałe. Dlatego jeśli miejsca przemieszczania hello pobiera miejscami do środowiska produkcyjnego, będzie dziedziczyć ustawień aplikacji hello lokalnej pamięci podręcznej. Witaj miejscami nowo produkcji gniazdo będzie uruchamiana w lokalnej pamięci podręcznej powitania po kilku minutach i będzie można przygotowaniu miejsca jako część rozgrzewania miejsca po wymiany. Dlatego po zakończeniu wymiany gniazd hello Twojego miejsca produkcji będzie uruchomiony przed hello lokalnej pamięci podręcznej.

## <a name="frequently-asked-questions-faq"></a>Często zadawane pytania
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>Jak sprawdzić, czy lokalnej pamięci podręcznej stosuje toomy aplikacji sieci web?
Jeśli aplikacja sieci web powinien niezwykle wydajny i niezawodny magazyn zawartości, nie używa hello magazynu zawartości toowrite najważniejszych danych w czasie wykonywania i łączny rozmiar jest mniejszy niż 2 GB, następnie hello odpowiedź brzmi "tak"! tooget hello całkowity rozmiar folderów /site i /siteextensions, można użyć rozszerzenia lokacji hello "Użycie dysku aplikacji sieci Web platformy Azure".  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>Jak sprawdzić, czy Moja witryna zastąpiono toousing lokalnej pamięci podręcznej?
Jeśli używasz funkcji lokalnej pamięci podręcznej hello ze środowiska przejściowe, operacja zamiany hello nie zostanie ukończona, aż do lokalnej pamięci podręcznej jest przygotowaniu miejsca. toocheck, jeśli witryna jest hostowana na lokalnej pamięci podręcznej, można sprawdzić zmiennej środowiskowej proces roboczy hello `WEBSITE_LOCALCACHE_READY`. Użyj instrukcji hello na powitania [zmiennej środowiskowej proces roboczy](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) tooaccess strony hello zmiennej środowiskowej procesu roboczego na wiele wystąpień.  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>Po opublikowaniu tylko nowych zmian, ale Moja aplikacja sieci web nie wydaje się toohave je. Dlaczego?
Jeśli aplikacja sieci web korzysta z lokalnej pamięci podręcznej, następnie należy toorestart lokacji tooget hello najnowsze zmiany. Nie ma lokacji produkcyjnej tooa zmiany toopublish? Zobacz Opcje miejsca hello hello poprzedniej najlepszych praktyk sekcji.

### <a name="where-are-my-logs"></a>Gdzie znajdują się Moje dzienniki?
Z lokalnej pamięci podręcznej folderów danych i dzienniki wyglądać nieco inaczej. Jednak hello struktury sieci pozostaje podfoldery hello takie same, z tą różnicą, że podfoldery hello są nestled w obszarze podfolder o hello formatu "Unikatowy identyfikator maszyny Wirtualnej" + sygnatury czasowej.

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>Mam włączoną lokalnej pamięci podręcznej, ale aplikacja sieci web nadal pobiera uruchomiony ponownie. Dlaczego jest to, że? Myślę, że pomogła lokalnej pamięci podręcznej z częste aplikacji zostanie ponownie uruchomiony.
Lokalnej pamięci podręcznej pomagać w zapobieganiu ponownego uruchomienia aplikacji dotyczące magazynu w sieci web. Jednak aplikacja sieci web można nadal przechodzą ponownego uruchomienia podczas zaplanowanej infrastruktury uaktualnienia hello maszyny Wirtualnej. Witaj ogólną ponowne uruchomienia aplikacji, które występują z lokalnej pamięci podręcznej włączone powinna być mniej.

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>Lokalnej pamięci podręcznej wyklucza wszelkie katalogi możliwość skopiowane toohello szybciej dysku lokalnego?
W ramach kroku hello, który kopiuje zawartość magazynu hello folderu o nazwie repozytorium zostaną wykluczone. Pomaga to w scenariuszach, w którym zawartości witryny może zawierać repozytorium kontroli źródła, który nie może być wymagany w operacji tooday dzień hello aplikacji sieci web. 
