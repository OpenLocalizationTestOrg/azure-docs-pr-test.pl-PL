---
title: "Klonowanie aplikacji sieci Web przy użyciu portalu Azure"
description: "Dowiedz się, jak klonowanie aplikacji sieci Web do nowej aplikacji sieci Web przy użyciu portalu Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Usługa aplikacji Azure aplikacji klonowania za pomocą portalu Azure
Funkcję klonowania w [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) umożliwia łatwe Sklonowanie istniejących sieci web aplikacji do nowo utworzonej aplikacji w innym regionie lub w tym samym regionie. Umożliwi to klienci mogą wdrożyć wiele aplikacji w różnych regionach, szybkie i łatwe.

Klonowanie aplikacji jest obecnie obsługiwany tylko w przypadku planów usługi aplikacji warstwy premium. Nowa funkcja używa tego samego ograniczenia jako funkcja kopii zapasowej aplikacji sieci Web, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Klonowanie istniejącej aplikacji
Aplikacja sieci web musi być uruchomiona **Premium** trybu, aby możliwe utworzenia klona dla aplikacji sieci web.

1. W [Azure Portal](https://portal.azure.com/), otwarcie bloku aplikacji sieci web.
2. Kliknij przycisk **narzędzia**. Następnie w **narzędzia** bloku, kliknij przycisk **aplikacji w klonowania**.
   
    ![][1]
   
   > [!NOTE]
   > Jeśli aplikacja sieci web nie jest już w **Premium** tryb, zostanie wyświetlony komunikat informujący o obsługiwanych tryby w klonowania aplikacji. W tym momencie masz możliwość wybrania **uaktualnienia**.
   > 
   > 
3. W **aplikacji w klonowania** bloku Podaj nazwę nowej aplikacji sieci web, grupy zasobów i Plan usługi App Service. Również użytkownik będzie mógł zdecydować się na potrzeby klonowania szereg ustawień aplikacji sieci web źródła lub nie.
   
    ![][2]
4. Po kliknięciu przycisku **utworzyć** platformy rozpoczęcia pracy na tworzenie własnego klonu źródłowej aplikacji sieci web.

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a>Klonowanie istniejącej aplikacji do środowiska usługi aplikacji
W **aplikacji w klonowania** bloku klienta będzie mieć możliwość wyboru z puli aplikacji w istniejącym środowisku usługi aplikacji.

## <a name="current-restrictions"></a>Bieżące ograniczenia
Ta funkcja jest obecnie w przeglądzie, pracujemy, aby dodać nowe funkcje w czasie, poniżej są znane ograniczenia dotyczące obsługi bieżącego klonowania aplikacji w portalu Azure:

* Ustawienia usługi Azure Traffic Manager nie są klonowane.
* Ustawienia skalowania automatycznego nie są klonowane.
* Ustawienia harmonogramu tworzenia kopii zapasowej nie są klonowane.
* Ustawienia sieci Wirtualnej nie są klonowane.
* Wgląd w aplikację nie są automatycznie skonfigurowane na docelowej aplikacji sieci web
* Łatwe ustawienia uwierzytelniania nie są klonowane.
* Program kudu rozszerzenia nie są klonowane.
* Porada reguły nie są klonowane.
* Baza danych zawartości nie są klonowane.

### <a name="references"></a>Dokumentacja
* [Klonowanie aplikacji sieci Web przy użyciu programu PowerShell](app-service-web-app-cloning.md)
* [Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md)
* [Jak utworzyć środowisko App Service Environment](app-service-web-how-to-create-an-app-service-environment.md)
* [Tworzenie aplikacji sieci Web w środowisku usługi App Service](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Wprowadzenie do usługi App Service Environment](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
