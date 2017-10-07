---
title: "aaaGuidance związane z opracowywaniem usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Poznaj pojęcia dotyczące usługi Azure Functions hello i techniki potrzebnych funkcji toodevelop na platformie Azure, we wszystkich językach programowania i powiązania."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Funkcje przewodnik azure Developer, funkcje, przetwarzania elementów webhook, dynamiczne obliczeń, architektura niekorzystającą zdarzeń"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Przewodnik dla deweloperów funkcji platformy Azure
W środowisku Azure Functions określonych funkcji udostępniania kilka podstawowe koncepcje techniczne i składników, niezależnie od języka hello lub powiązanie, którego używasz. Przed możesz przejść do uczenia szczegóły tooa określonego języka lub powiązanie, należy się tooread przez ten przegląd, w którym ma zastosowanie tooall z nich.

W tym artykule przyjęto, że został już przeczytany hello [Azure Functions — omówienie](functions-overview.md) i zapoznaniu się z [pojęcia zestaw SDK zadań Webjob wyzwalaczy, powiązania i środowiska uruchomieniowego JobHost hello](../app-service-web/websites-dotnet-webjobs-sdk.md). Środowisko Azure Functions opiera się na powitania zestaw SDK zadań Webjob. 

## <a name="function-code"></a>Kod — funkcja
A *funkcja* hello koncepcja podstawowego w usługi Azure Functions. Pisanie kodu dla funkcji w języku wybranym i Zapisz kod hello i pliki konfiguracyjne w hello w tym samym folderze. nosi nazwę konfiguracji Hello `function.json`, który zawiera dane konfiguracyjne w formacie JSON. Różnych języków są obsługiwane, a każda z nich ma toowork nieco inne środowisko zoptymalizowanych pod kątem najlepsze dla tego języka. 

Plik function.json Hello definiuje powiązania funkcji hello i innych ustawień konfiguracyjnych. środowiska uruchomieniowego Hello korzysta z tego pliku toodetermine hello zdarzenia toomonitor i sposób wykonywania funkcji toopass dane i zwracanych danych z. Witaj poniżej znajduje się przykładowy plik function.json.

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

Zestaw hello `disabled` właściwości zbyt`true` funkcja hello tooprevent wstrzymywane.

Witaj `bindings` właściwość jest, którym możesz skonfigurować zarówno wyzwalaczy i powiązań. Każdego powiązania udostępnia kilka typowych ustawień i niektórych ustawień, które są określone tooa określonego typu powiązania. Każde powiązanie wymaga hello następujące ustawienia:

| Właściwość | Wartości/typów | Komentarze |
| --- | --- | --- |
| `type` |Ciąg |Typ wiązania. Na przykład `queueTrigger`. |
| `direction` |"in" "out" |Wskazuje, czy powiązanie hello jest odbierania danych w funkcji hello lub wysyłanie danych z hello funkcji. |
| `name` |Ciąg |Nazwa Hello jest używany dla hello powiązanych danych w funkcji hello. Język C# jest to nazwa argumentu; dla języka JavaScript tego klucza hello na liście klucza i wartości. |

## <a name="function-app"></a>Funkcja aplikacji
Aplikacja funkcji składa się z co najmniej jeden poszczególne funkcje, które są ze sobą zarządzane przez usługę Azure App Service. Wszystkie funkcje hello w udziale, funkcja aplikacji hello samej cenową planu, ciągłe wdrażanie i wersji środowiska wykonawczego. Funkcje zapisywane w wielu językach można udostępnić wszystkie hello sam funkcji aplikacji. Należy traktować jako tooorganize sposób aplikacji funkcji i zbiorczo zarządzania funkcjami. 

## <a name="runtime-script-host-and-web-host"></a>Środowisko uruchomieniowe (host skryptów i hosta sieci web)
środowisko uruchomieniowe Hello lub host skryptów jest hello podstawowy zestaw SDK zadań Webjob host, na którym nasłuchuje zdarzeń, zbiera i wysyła dane, a ostatecznie uruchamia kod. 

Wyzwalacze toofacilitate HTTP jest również hosta sieci web, który jest zaprojektowana toosit przed hello host skryptów w scenariuszach produkcji. Mając dwa hosty pomaga hostem skryptów hello tooisolate ruchu frontonu hello zarządza hello hosta sieci web.

## <a name="folder-structure"></a>Struktura folderów
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

Podczas tworzenia projektu wdrażania funkcji tooa funkcji aplikacji w usłudze Azure App Service, możesz traktować tę strukturę folderów jako kodu lokacji. Możesz użyć istniejących narzędzi, takich jak ciągłej integracji i wdrażania lub skrypty niestandardowe wdrożenie może wdrożyć czasu pakietu instalacji lub kod transpilation.

> [!NOTE]
> Upewnij się, że toodeploy Twojego `host.json` plików i funkcja folderów bezpośrednio toohello `wwwroot` folderu. Nie dołączaj hello `wwwroot` folderu wdrożeń. W przeciwnym razie na końcu `wwwroot\wwwroot` folderów. 
> 
> 

## <a id="fileupdate"></a>Jak tooupdate funkcji pliki aplikacji
Edytor funkcja Hello wbudowane hello portalu Azure umożliwia uaktualnienie hello *function.json* plików i hello pliku kodu dla funkcji. tooupload lub aktualizacji dla innych, takie jak pliki *package.json* lub *project.json* ani zależności, masz toouse innych metod wdrażania.

Funkcja aplikacje są tworzone w usłudze aplikacji, więc wszystkie hello [aplikacje sieci web toostandard dostępne opcje wdrożenia](../app-service-web/web-sites-deploy.md) są także dostępne dla funkcji aplikacji. Poniżej przedstawiono niektóre metody można użyć tooupload lub zaktualizować pliki aplikacji funkcji. 

#### <a name="toouse-app-service-editor"></a>toouse Edytor usługi aplikacji
1. W portalu Azure Functions hello, kliknij przycisk **funkcji ustawienia aplikacji**.
2. W hello **Zaawansowane ustawienia** kliknij **Przejdź ustawień usługi tooApp**.
3. Kliknij przycisk **Edytor usług aplikacji** w aplikacji Menu nawigacji w obszarze **narzędzi PROGRAMISTYCZNYCH**.
4. Kliknij przycisk **Przejdź**.
   
   Po załadowaniu Edytor usług aplikacji, zobaczysz hello *host.json* plików i funkcja foldery znajdujące się w *wwwroot*. 
5. Tooedit otwartych plików, lub przeciągnij i upuść z plików tooupload programowanie maszyny.

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>punkt końcowy SCM (Kudu) aplikacji toouse hello — funkcja
1. Przejdź do: `https://<function_app_name>.scm.azurewebsites.net`.
2. Kliknij przycisk **Konsola debugowania > CMD**.
3. Przejdź za`D:\home\site\wwwroot\` tooupdate *host.json* lub `D:\home\site\wwwroot\<function_name>` tooupdate pliki funkcji.
4. Przeciągnij i upuść plik ma tooupload do odpowiedniego folderu hello w siatce pliku hello. Istnieją dwa obszary siatki pliku hello, gdzie można usunąć pliku. Aby uzyskać *.zip* pliki, zostanie wyświetlone okno z etykietą hello "Przeciągnij tutaj tooupload i Rozpakuj." W przypadku innych typów plików porzucić hello pliku siatki, ale poza pole "Rozpakuj" hello.

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>toouse ciągłe wdrażanie
Wykonaj instrukcje hello w temacie hello [ciągłego wdrażania usługi Azure Functions](functions-continuous-deployment.md).

## <a name="parallel-execution"></a>Wykonywanie równoległe
Gdy wiele wyzwalająca zdarzenia występują szybciej, niż może je przetwarzać runtime jednowątkowe funkcji, środowiska uruchomieniowego hello może wywołanie funkcji hello wielokrotnie równolegle.  Jeśli aplikacja funkcji używa hello [zużycie plan hostingu](functions-scale.md#how-the-consumption-plan-works), hello funkcji aplikacji może automatycznie skalować w poziomie.  Każde wystąpienie hello funkcji aplikacji, czy aplikacja hello jest uruchamiana na hello zużycie hosting planu lub zwykły [usługi aplikacji — plan hostingu](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), może przetwarzać funkcja współbieżnych wywołań z użyciem wielu wątków.  Hello maksymalną liczbę funkcji współbieżnych wywołań w każdym wystąpieniu aplikacji funkcji zależy od typu hello wyzwalacza używane oraz hello zasoby używane przez inne funkcje w hello funkcji aplikacji.

## <a name="functions-runtime-versioning"></a>Funkcje wersji środowiska uruchomieniowego

Można skonfigurować hello wersji środowiska uruchomieniowego funkcje hello przy użyciu hello `FUNCTIONS_EXTENSION_VERSION` ustawienia aplikacji. Na przykład hello wartość "~ 1" wskazuje, czy Twoja aplikacja funkcja będzie używać 1 jako jego wersji głównej. Funkcja aplikacji są nowa wersja pomocnicza tooeach uaktualniony po ich wydaniu. Witaj dokładnej wersji aplikacji funkcji można wyświetlić w hello **ustawienia** kartę w hello portalu Azure.

## <a name="repositories"></a>Repozytoria
Witaj kodu dla usługi Azure Functions to typu open source i przechowywane w repozytoriów GitHub:

* [Środowisko uruchomieniowe Functions Azure](https://github.com/Azure/azure-webjobs-sdk-script/)
* [Portalu Azure Functions](https://github.com/projectkudu/AzureFunctionsPortal)
* [Szablony funkcji platformy Azure](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [Zestaw SDK zadań Webjob Azure](https://github.com/Azure/azure-webjobs-sdk/)
* [Zestaw SDK zadań Webjob Azure rozszerzeń](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>Powiązania
W tym miejscu znajduje się tabela wszystkie obsługiwane powiązania.

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>Zgłaszanie problemów
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji zobacz następujące zasoby hello:

* [Najlepsze rozwiązania dotyczące usługi Azure Functions](functions-best-practices.md)
* [Azure dokumentacja dla deweloperów funkcje C#](functions-reference-csharp.md)
* [Azure dokumentacja dla deweloperów funkcje F #](functions-reference-fsharp.md)
* [Dokumentacja dla deweloperów NodeJS funkcji platformy Azure](functions-reference-node.md)
* [Azure funkcje wyzwalaczy i powiązań](functions-triggers-bindings.md)
* [Środowisko Azure Functions: hello podróży](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) na blogu zespołu hello Azure App Service. Historia jak został opracowany usługi Azure Functions.

