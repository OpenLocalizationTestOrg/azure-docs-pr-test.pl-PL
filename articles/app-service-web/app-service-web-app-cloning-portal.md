---
title: "aaaWeb w klonowania aplikacji przy użyciu portalu Azure"
description: "Dowiedz się, jak tooclone toonew Twojej aplikacji sieci Web aplikacji sieci Web przy użyciu portalu Azure."
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
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Usługa aplikacji Azure aplikacji klonowania za pomocą portalu Azure
Funkcja w klonowania Hello [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) umożliwia łatwe sklonować istniejącej aplikacji sieci web apps tooa nowo utworzony w innym regionie lub hello tego samego regionu. Spowoduje to włączenie toodeploy klientów liczba aplikacji w różnych regionach, szybkie i łatwe.

Klonowanie aplikacji jest obecnie obsługiwany tylko w przypadku planów usługi aplikacji warstwy premium. Hello nowej używa funkcji hello takie same ograniczenia co funkcja kopii zapasowej aplikacji sieci Web, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Klonowanie istniejącej aplikacji
Witaj aplikacji sieci web musi być uruchomiona w hello **Premium** tryb aby toocreate klonowania dla aplikacji sieci web hello.

1. W hello [Azure Portal](https://portal.azure.com/), otwarcie bloku aplikacji sieci web.
2. Kliknij przycisk **narzędzia**. Następnie w hello **narzędzia** bloku, kliknij przycisk **aplikacji w klonowania**.
   
    ![][1]
   
   > [!NOTE]
   > Jeśli hello aplikacji sieci web nie jest już hello **Premium** tryb, zostanie wyświetlony komunikat informujący o hello obsługiwane tryby aplikacji klonowania. W tym momencie masz hello opcja tooselect **uaktualnienia**.
   > 
   > 
3. W hello **aplikacji w klonowania** bloku Podaj nazwę nowej aplikacji sieci web hello, grupy zasobów i Plan usługi App Service. Również hello użytkownik będzie możliwe toochoose czy tooclone szereg ustawień aplikacji sieci web źródła lub nie.
   
    ![][2]
4. Po kliknięciu przycisku **utworzyć** platformy hello rozpoczęcia pracy na tworzenie własnego klonu hello źródłowej aplikacji sieci web.

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Klonowanie tooan aplikacji istniejącego środowiska usługi aplikacji
W hello **aplikacji w klonowania** bloku powitania klienta będzie mieć hello opcja toochoose puli aplikacji w istniejącym środowisku usługi aplikacji.

## <a name="current-restrictions"></a>Bieżące ograniczenia
Ta funkcja jest obecnie w przeglądzie, pracujemy nad tooadd nowe funkcje w czasie, następujące listy hello są hello znane ograniczenia dotyczące obsługi bieżącego hello klonowania aplikacji w portalu Azure:

* Ustawienia usługi Azure Traffic Manager nie są klonowane.
* Ustawienia skalowania automatycznego nie są klonowane.
* Ustawienia harmonogramu tworzenia kopii zapasowej nie są klonowane.
* Ustawienia sieci Wirtualnej nie są klonowane.
* Wgląd w aplikację nie są automatycznie skonfigurowane w aplikacji sieci web docelowym hello
* Łatwe ustawienia uwierzytelniania nie są klonowane.
* Program kudu rozszerzenia nie są klonowane.
* Porada reguły nie są klonowane.
* Baza danych zawartości nie są klonowane.

### <a name="references"></a>Dokumentacja
* [Klonowanie aplikacji sieci Web przy użyciu programu PowerShell](app-service-web-app-cloning.md)
* [Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md)
* [Jak tooCreate środowiska usługi aplikacji](app-service-web-how-to-create-an-app-service-environment.md)
* [Tworzenie aplikacji sieci Web w środowisku usługi App Service](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Wprowadzenie tooApp środowiska usługi](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
