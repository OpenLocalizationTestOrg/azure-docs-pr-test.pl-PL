---
title: aaaConfigure ustawienia aplikacji funkcji platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconfigure Azure funkcji ustawienia aplikacji."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>Jak toomanage aplikacji funkcji w hello portalu Azure 

W środowisku Azure Functions aplikacji funkcji udostępnia hello kontekstu wykonywania dla poszczególnych funkcji. Funkcja zachowania aplikacji zastosować tooall funkcje obsługiwane przez aplikację danej funkcji. W tym temacie opisano sposób tooconfigure i zarządzania aplikacjami funkcji w hello portalu Azure.

toobegin, przejdź toohello [portalu Azure](http://portal.azure.com) i zaloguj się na tooyour konto platformy Azure. Na pasku wyszukiwania hello u góry hello hello portalu wpisz nazwę hello aplikacji funkcji, a następnie wybierz go z listy hello. Po wybraniu aplikacji funkcji, zobacz temat hello następujące strony:

![Funkcja Przegląd aplikacji w portalu Azure hello](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>Karta Ustawienia aplikacji — funkcja

![Funkcja aplikacji — omówienie hello portalu Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

Witaj **ustawienia** karta jest, której można zaktualizować wersji środowiska uruchomieniowego funkcje hello używany przez aplikację funkcji. Możliwe jest również, w których zarządzasz hello hosta kluczy używanych toorestrict HTTP dostępu tooall funkcji obsługiwanych przez hello funkcji aplikacji.

Funkcje obsługuje hosting zużycia i hosting planów usługi aplikacji. Aby uzyskać więcej informacji, zobacz [wybierz hello plan prawidłowe usługi Azure Functions](functions-scale.md). Dla lepszej przewidywalności w planie zużycie hello funkcje umożliwia ograniczenie użycia platformy ustawiając dziennego limitu przydziału wykorzystania w gigabajtach sekund. Po osiągnięciu limitu przydziału wykorzystania codzienne hello hello funkcja aplikacja została zatrzymana. Aplikacja funkcji zatrzymana w wyniku osiągnięcia hello wydatków przydziału można ją ponownie włączyć z hello tego samego kontekstu ustalaniu hello codziennie wydatków przydziału. Zobacz hello [usługi Azure Functions cennikiem](http://azure.microsoft.com/pricing/details/functions/) szczegółowe informacje dotyczące rozliczeń.   

## <a name="platform-features-tab"></a>Karta funkcje platformy

![Funkcja kartę funkcje platformy aplikacji.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

Funkcja aplikacje uruchomione w i są obsługiwane przez platformę Azure App Service hello. Tak funkcja aplikacji ma toomost dostęp do funkcji hello hosting platformy podstawowej platformy Azure w sieci Web. Witaj **funkcji platformy** jest karta gdzie dostęp hello wiele funkcji hello platformie App Service, używanego w aplikacjach funkcji. 

> [!NOTE]
> Nie wszystkie funkcje usługi aplikacji są dostępne, po uruchomieniu aplikacji funkcji dla planu hostingu hello zużycia.

Witaj pozostałej części tego tematu koncentruje się na powitania następujące funkcje usługi aplikacji hello portalu Azure, które są przydatne w przypadku funkcji:

+ [Edytor usługi aplikacji](#editor)
+ [Ustawienia aplikacji](#settings) 
+ [Console](#console)
+ [Zaawansowane narzędzia (Kudu)](#kudu)
+ [Opcje wdrażania](#deployment)
+ [CORS](#cors)
+ [Uwierzytelnianie](#auth)
+ [Definicja interfejsu API](#swagger)

Aby uzyskać więcej informacji o tym, jak toowork z ustawieniami usługi App Service, zobacz [Konfigurowanie ustawień usługi aplikacji Azure](../app-service-web/web-sites-configure.md).

### <a name="editor"></a>Edytor usługi aplikacji

| | |
|-|-|
| ![Funkcja aplikacji edytora usługi aplikacji.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | Edytor usług aplikacji Hello jest Zaawansowany edytor w portalu można pliki konfiguracji JSON toomodify i podobne plików kodu. Wybranie tej opcji spowoduje uruchomienie na karcie przeglądarki oddzielne za pomocą edytora podstawowego. Umożliwia toointegrate hello Git repozytorium, uruchom i debugowania kodu i modyfikowanie ustawień funkcji aplikacji. Tego edytora udostępnia środowisko deweloperskie rozszerzone do funkcji w porównaniu z bloku aplikacji funkcja domyślne hello.    |

![Witaj edytora usługi aplikacji](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>Ustawienia aplikacji

| | |
|-|-|
| ![Funkcja aplikacji ustawienia aplikacji.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | Usługi aplikacji Hello **ustawienia aplikacji** bloku jest gdzie Konfigurowanie i zarządzanie nimi framework w wersji, debugowania zdalnego, ustawienia aplikacji i parametry połączenia. Po zintegrowaniu aplikacji funkcji z innymi usługami innych firm i Azure można modyfikować tych ustawień w tym miejscu. |

![Konfigurowanie ustawień aplikacji](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>Konsoli

| | |
|-|-|
| ![Funkcja konsoli aplikacji hello portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | Hello konsoli w portalu jest narzędziem idealne developer, zamiast toointeract z aplikacją funkcji z wiersza polecenia hello. Typowe polecenia obejmują katalogu i tworzenie plików i nawigacji, a także wykonywanie plików wsadowych i skryptów. |

![Funkcja aplikacji konsoli](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>Zaawansowane narzędzia (Kudu)

| | |
|-|-|
| ![Funkcja aplikacji Kudu w hello portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | Witaj zaawansowanych narzędzi dla aplikacji usługi (znanej także jako Kudu) zapewniać dostęp do funkcji administracyjnych tooadvanced aplikacji funkcji. Program Kudu do zarządzania informacje o systemie, ustawienia aplikacji, zmienne środowiskowe, rozszerzenia lokacji, nagłówków HTTP i zmiennych serwera. Można również uruchomić **Kudu** przechodząc tak samo, jak punkt końcowy SCM toohello dla funkcji aplikacji,`https://<myfunctionapp>.scm.azurewebsites.net/` |

![Skonfiguruj Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">Opcje wdrażania

| | |
|-|-|
| ![Funkcja opcje wdrażania aplikacji w portalu Azure hello](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | Funkcje pozwala tworzyć kodu funkcji na komputerze lokalnym. Następnie możesz przekazać tooAzure projektu aplikacji sieci funkcja lokalna. Ponadto tootraditional FTP przekazywania, funkcje umożliwia wdrażanie aplikacji przy użyciu rozwiązań popularnych ciągłej integracji, takich jak GitHub, programu VSTS Dropbox, Bitbucket i innych funkcji. Aby uzyskać więcej informacji, zobacz [ciągłego wdrażania usługi Azure Functions](functions-continuous-deployment.md). tooupload ręcznie przy użyciu FTP lub lokalnego Git, musi również [skonfigurować poświadczenia wdrażania](functions-continuous-deployment.md#credentials). |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![Funkcja aplikacji CORS w portalu Azure hello](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | uruchomienie złośliwego kodu tooprevent w usługach, bloki usługi aplikacji wywołuje tooyour funkcji aplikacji ze źródeł zewnętrznych. Funkcje obsługuje współużytkowanie zasobów między źródłami udostępnianie toolet (CORS), można zdefiniować "listą dozwolonych" dozwolone źródła, z których funkcji można zaakceptować żądania zdalne.  |

![Konfigurowanie funkcji aplikacji CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>Uwierzytelnianie

| | |
|-|-|
| ![Funkcja uwierzytelniania aplikacji hello portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | Korzystając z funkcji wyzwalacz protokołu HTTP, można wymagać wywołania toofirst należy uwierzytelnieni. Usługi aplikacji obsługuje uwierzytelnianie usługi Azure Active Directory i zaloguj się przy użyciu dostawców sieci społecznościowych, takich jak Facebook, firma Microsoft i Twitter. Aby uzyskać więcej informacji na temat konfigurowania uwierzytelniania określonych dostawców, zobacz [omówienie uwierzytelniania w usłudze Azure App Service](../app-service/app-service-authentication-overview.md). |

![Konfigurowanie uwierzytelniania dla aplikacji funkcja](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>Definicja interfejsu API

| | |
|-|-|
| ![Funkcja aplikacji API programu swagger definicji w hello portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | Funkcje obsługuje struktury Swagger toomore klientów tooallow łatwo korzystać z funkcji wyzwalanych przez protokół HTTP. Aby uzyskać więcej informacji na temat tworzenia definicji interfejsu API z programu Swagger, odwiedź stronę [wprowadzenie do aplikacji interfejsu API, ASP.NET i struktury Swagger na platformie Azure](../app-service-api/app-service-api-dotnet-get-started.md). Umożliwia także funkcje proxy toodefine pojedynczą powierzchnię interfejsu API dla wielu funkcji. Aby uzyskać więcej informacji, zobacz [Praca z serwerów proxy funkcji Azure](functions-proxies.md). |

![Konfigurowanie funkcji aplikacji interfejsu API](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>Następne kroki

+ [Konfigurowanie ustawień usługi aplikacji Azure](../app-service-web/web-sites-configure.md)
+ [Ciągłe wdrażanie dla usługi Azure Functions](functions-continuous-deployment.md)



