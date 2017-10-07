---
title: "tooScale aaaHow aplikacji w środowisku usługi aplikacji"
description: "Skalowanie aplikacji w środowisku usługi aplikacji"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>Skalowanie aplikacji w środowisku usługi App Service
Witaj w usłudze Azure App Service są zwykle trzy czynności, które można skalować:

* Cennik planu
* rozmiar procesu roboczego 
* Liczba wystąpień.

W elemencie ASE nie ma bez konieczności tooselect lub zmień hello cenową planu.  Pod względem możliwości jest już na poziomie możliwości cenowej Premium dostępne.  

Za pomocą względem tooworker rozmiary Witaj, Administratorze ASE można przypisać hello rozmiar toobe zasobów obliczeniowych hello używane dla każdej puli procesów roboczych.  Czy oznacza, że proces roboczy puli 1 z P4 zasobów obliczeniowych i proces roboczy puli 2 z P1 zasoby obliczeniowe, w razie potrzeby.  Nie mają toobe w kolejności rozmiar.  Szczegółowe informacje wokół hello rozmiary i ich cen można znaleźć tutaj dokumentu hello [Azure App Service — ceny][AppServicePricing].  Spowoduje to pozostawienie hello skalowanie opcje dla aplikacji sieci web i plany usługi App Service w toobe środowiska usługi aplikacji:

* proces roboczy puli zaznaczenia
* Liczba wystąpień

Zmiana oba elementy odbywa się za pośrednictwem hello potrzeby pokazywane dla Twojego ASE hostowanej plany usługi App Service interfejsu użytkownika.  

![][1]

Nie można skalować strona ASP poza hello liczba zasobów obliczeniowych dostępnych w puli procesów roboczych hello, który jest strona ASP.  Jeśli należy obliczyć zasobów w tej puli procesów roboczych należy tooget Twojego tooadd administratora ASE je.  Aby odczytać informacji wokół ponowne konfigurowanie Twojego ASE tutaj informacje hello: [jak tooConfigure środowiska usługi aplikacji][HowtoConfigureASE].  Można również tootake zaletą hello ASE skalowania automatycznego funkcji tooadd pojemności na podstawie harmonogramu lub metryki.  więcej informacji na temat konfigurowania automatycznego skalowania dla środowiska hello ASE, się, zobacz tooget [jak tooconfigure funkcja automatycznego skalowania dla środowiska usługi aplikacji][ASEAutoscale].

Można utworzyć wiele aplikacji przy użyciu zasobów obliczeniowych od pule procesów roboczych różnych planów usługi lub skorzystać z tej samej puli procesów roboczych hello.  Przykład, jeśli masz (10) zasobów obliczeniowych dostępnych w procesu roboczego puli 1, można wybrać toocreate jeden plan usługi app service przy użyciu zasobów obliczeniowych (6) i planowanie drugi usługi aplikacji, która używa zasobów obliczeniowych (4).

### <a name="scaling-hello-number-of-instances"></a>Skalowanie hello liczba wystąpień
Podczas tworzenia aplikacji sieci web w środowisku usługi aplikacji rozpoczyna się od 1 wystąpienie.  Mogą być następnie skalowania w poziomie tooprovide wystąpień tooadditional dodatkowe zasoby dla aplikacji obliczeniowe.   

Jeśli Twoje ASE ma wystarczającą wydajność to bardzo proste.  Możesz przejść tooyour planu usługi App Service przechowujący witryn hello tooscale się a wybrać skali.  Spowoduje to otwarcie hello interfejsu użytkownika, których można ręcznie ustawić hello skalowania dla strona ASP lub konfigurowanie reguł automatycznego skalowania dla Twojego środowiska ASP.  aplikację po prostu zestaw skalowania toomanually ***skalowanie przez*** za***liczba wystąpień ustawiana ręcznie***.  W tym miejscu przeciągnij hello suwaka toohello wymaganą ilość lub wprowadzić w hello pole dalej toohello suwaka.  

![][2] 

Hello reguły automatycznego skalowania dla środowiska ASP, w pracach ASE hello takie same, jak zwykle.  Możesz wybrać ***procent użycia procesora CPU*** w obszarze ***skalowanie przez*** i utworzyć zasady automatycznego skalowania do programu ASP na podstawie procent użycia procesora CPU lub można utworzyć bardziej złożone zasady przy użyciu ***reguły wydajności i harmonogram***.  toosee ukończyć bardziej szczegółowe informacje na temat konfigurowania przewodnik hello Użyj skalowania automatycznego tutaj [skalować aplikację w usłudze Azure App Service][AppScale]. 

### <a name="worker-pool-selection"></a>Proces roboczy puli zaznaczenia
Jak wspomniano wcześniej, hello procesu roboczego puli wybór jest dostępny hello ASP interfejsu użytkownika.  Otwarcie bloku hello hello ASP mają tooscale, a następnie wybierz puli procesów roboczych.  Są wyświetlane wszystkie hello pule procesów roboczych, które zostały skonfigurowane w środowisku usługi aplikacji.  Jeśli masz tylko jednego procesu roboczego puli będzie tylko Zobacz hello jednej puli na liście.  toochange jakiego procesu roboczego puli strona ASP, należy po prostu wybierz ma toomove Twojego planu usługi App Service, do puli procesów roboczych hello.  

![][3]

Przed przeniesieniem strona ASP z jednego procesu roboczego puli tooanother jest ważne toomake upewnić się, że będzie odpowiedniej wydajności dla Twojego środowiska ASP.  Na liście hello pule procesów roboczych nie tylko znajduje się nazwa puli worker hello, ale możesz też sprawdzić liczbę pracowników są dostępne w tej puli procesów roboczych.  Upewnij się, że ma wystarczającej liczby dostępnych toocontain wystąpień planu usługi aplikacji.  Jeśli zasoby w puli procesów roboczych hello wymagają więcej obliczeniowe mają toomove uzyskanie, następnie tooadd administratora Twojej ASE je.  

> [!NOTE]
> Uruchamia przeniesienie spowoduje, że chłodni ASP z jednego procesu roboczego puli aplikacji hello w ASP.  Może to spowodować toorun żądań powoli aplikacji jest zimnych uruchomiona na powitania nowych zasobów obliczeniowych.  Witaj zimny start można uniknąć przy użyciu hello [aplikacji ciepłych się możliwość] [ AppWarmup] w usłudze Azure App Service.  Moduł Inicjowanie aplikacji Hello opisaną w artykule hello działa także dla zimnych startów ponieważ proces inicjowania hello również jest wywoływane, gdy aplikacje są zimnych uruchomiona na nowe zasoby obliczeniowe. 
> 
> 

## <a name="getting-started"></a>Wprowadzenie
tooget wprowadzenie do środowiska usługi App Service, zobacz [jak tooCreate środowiska usługi aplikacji][HowtoCreateASE]

Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
