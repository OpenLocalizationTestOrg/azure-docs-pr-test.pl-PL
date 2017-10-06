---
title: "aaaCreate aplikacji sieci web w wersji 1 środowiska usługi aplikacji"
description: "Dowiedz się, jak toocreate sieci web, aplikacji i planów usługi aplikacji w wersji 1 środowiska usługi aplikacji"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>Tworzenie aplikacji sieci web w wersji 1 środowiska usługi aplikacji

> [!NOTE]
> Ten artykuł dotyczy hello v1 środowiska usługi aplikacji.  Istnieje nowsza wersja hello środowiska usługi aplikacji jest łatwiejsze toouse, który jest uruchamiany na bardziej zaawansowanych infrastruktury. więcej informacji na temat nowej wersji hello rozpoczynać hello toolearn [toohello wprowadzenie środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak aplikacje sieci web na toocreate i planów usługi App Service w [v1 środowiska usługi aplikacji](app-service-app-service-environment-intro.md) (ASE). 

> [!NOTE]
> Jeśli chcesz toolearn jak toocreate aplikacji sieci web, ale nie muszą toodo go w środowisku usługi aplikacji, zobacz [utworzenia aplikacji sieci web .NET](app-service-web-get-started-dotnet.md) lub jeden z hello powiązanych samouczków dla innych języków i struktur.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
W tym samouczku założono, że utworzono środowiska usługi aplikacji. Jeśli użytkownik jeszcze nie, zobacz [tworzenie środowiska usługi aplikacji](app-service-web-how-to-create-an-app-service-environment.md). 

## <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web
1. W hello [Azure Portal](https://portal.azure.com/), kliknij przycisk **nowe > sieci Web i mobilność > Aplikacja sieci Web**. 
   
    ![][1]
2. Wybierz subskrypcję.  
   
    Jeśli masz wiele subskrypcji, należy pamiętać, tym toocreate jako aplikacji w środowisku usługi aplikacji, należy toouse hello tej samej subskrypcji, który został użyty podczas tworzenia środowiska hello. 
3. Wybierz lub utwórz grupę zasobów.
   
    *Grupy zasobów* umożliwiają możesz toomanage powiązanych zasobów platformy Azure jako jednostki i są przydatne podczas ustanawiania *kontroli dostępu opartej na rolach* reguły (RBAC) dla aplikacji. Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager][ResourceGroups]. 
4. Wybierz lub Utwórz plan usługi aplikacji.
   
    *Planów usługi App Service* zarządzanych zestawów aplikacji sieci web.  Zwykle po wybraniu cennika, hello pobierana jest toohello zastosowanych planów usługi aplikacji zamiast toohello poszczególnych aplikacji. W elemencie ASE opłacać obliczeń hello wystąpień przydzielone toohello ASE zamiast co zostały wymienione w Twojej aplikacji ASP.  tooscale hello liczby wystąpień aplikacji sieci web skalowanie w górę hello wystąpień planu usługi aplikacji i ma wpływ na wszystkie aplikacje sieci web hello w tym planie.  Niektóre funkcje, takie jak witryny gniazda lub integracji sieci Wirtualnej również podlegają ograniczeniom ilość w ramach planu hello.  Aby uzyskać więcej informacji, zobacz [omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)
   
    Można zidentyfikować powitalne planów usługi App Service w Twojej ASE, analizując hello lokalizacji, która jest odnotowany w obszarze Nazwa planu hello.  
   
    ![][5]
   
    Jeśli chcesz toouse plan usługi aplikacji, która już istnieje w środowisku usługi aplikacji, wybierz plan. Jeśli chcesz toocreate nowy plan usługi aplikacji, zobacz hello następujące części tego samouczka [Utwórz plan usługi aplikacji w środowisku usługi aplikacji](#createplan).
5. Wprowadź nazwę powitania dla aplikacji sieci web, a następnie kliknij przycisk **Utwórz**. 
   
    Jeśli Twoje ASE używa adresu URL hello VIP zewnętrznych aplikacji w elemencie ASE: [*sitename*]. [ *Nazwa środowiska usługi aplikacji*]. p.azurewebsites.net zamiast [*sitename*]. azurewebsites.net
   
    Jeśli Twoje ASE używa wewnętrznego adresu VIP, a następnie hello adres URL aplikacji w tym jest ASE: [*sitename*]. [ *poddomeny określone podczas tworzenia ASE*]   
    Po wybraniu strona ASP podczas tworzenia ASE zobaczysz poddomeny hello zaktualizować poniżej **nazwy**

## <a name="createplan"></a>Tworzenie planu usługi aplikacji
Po utworzeniu planu usługi aplikacji w środowisku usługi aplikacji wybrane opcje procesu roboczego są różne, ponieważ w elemencie ASE nie nie udostępnionego pracowników.  masz toouse pracowników Hello są hello te, które zostały przydzielone toohello ASE przez administratora hello.  Oznacza to, że toocreate nowy plan, wymagają więcej procesów roboczych przydzielonych tooyour ASE puli procesów roboczych niż całkowita liczba wystąpień hello toohave we wszystkich planów już w tej puli procesów roboczych.  Jeśli nie ma wystarczającej liczby procesów roboczych w Twojej ASE procesu roboczego puli toocreate planu, należy toowork z Twojej tooget admin ASE, je dodać.

Inna różnica z planami usługi aplikacji obsługiwanych przez środowisko usługi aplikacji jest brak hello cennik zaznaczenia.  Jeśli masz środowisko usługi aplikacji płatność za zasoby obliczeniowe, używany przez hello system i nie masz dodano opłat za planów hello w tym środowisku.  Zwykle podczas tworzenia planu usługi App Service wybrać planu cenowego, która określa rozliczeniowego.  Środowiska usługi aplikacji jest zasadniczo lokalizację prywatnego umożliwiającego utworzenie zawartości.  Płacisz za hello środowiska i nie toohost zawartości.

Hello poniższe instrukcje przedstawiają sposób toocreate usługę aplikacji planowanie podczas tworzenia aplikacji sieci web, zgodnie z objaśnieniem w poprzedniej sekcji samouczka hello hello.

1. Kliknij przycisk **Utwórz nowy** w hello planu zaznaczenia interfejsu użytkownika i podaj nazwę dla planu, tak jak zwykle poza ASE.
2. Wybierz ASE hello mają toouse z Twojej lokalizacji selektora.
   
    Ponieważ środowisko usługi aplikacji jest zasadniczo lokalizacji prywatne wdrażanie, przedstawia on znajdujące się w lokalizacji. 
   
    ![][2]
   
    Po zaznaczeniu ASE w selektorze lokalizacji hello aktualizuje hello Tworzenie planu usługi aplikacji interfejsu użytkownika.  lokalizacji Hello teraz przedstawia nazwę hello hello ASE systemu i hello region znajduje się on w i hello cennik selektora plan jest zastępowany selektora puli procesu roboczego.  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>Wybieranie puli procesów roboczych
Zwykle w usłudze Azure App Service i poza nimi środowiska usługi aplikacji istnieje 3 rozmiary obliczeniowe, które są dostępne w przypadku zaznaczenia hello planu cenie dedykowanym.  W podobny sposób dla ASE można zdefiniować zapasowej pule too3 pracowników i określ rozmiar obliczeń hello, który jest używany dla tej puli procesów roboczych.  Co to oznacza to, w przypadku dzierżaw hello jest ASE zamiast zaznaczania planu cenowego o rozmiarze obliczeniowe dla planu usługi aplikacji, wybranym tak zwany *puli procesów roboczych*.  

Hello procesu roboczego puli wybór interfejsu użytkownika zawiera rozmiar obliczeń hello używany dla tej puli procesów roboczych poniżej hello nazwy.  Witaj dostępnej ilości odwołuje się toohow obliczeniowe wiele wystąpień są dostępne w tej puli.  Hello całkowitej puli faktycznie może mieć więcej wystąpień niż ta liczba, ale ta wartość oznacza toosimply ile nie są używane.  Jeśli potrzebujesz tooadjust tooadd Twojego środowiska usługi aplikacji obliczeniowe więcej zasobów, zobacz [Konfigurowanie środowiska usługi aplikacji](app-service-web-configure-an-app-service-environment.md).

![][4]

W tym przykładzie widać tylko dwa dostępne pule procesów roboczych. Wynika to z administratora ASE hello przydzielone tylko hosty w pulach tych dwóch procesu roboczego.  Witaj innej będzie wyświetlany, gdy są przydzielone do niej maszyny wirtualne.  

## <a name="after-web-app-creation"></a>Po utworzeniu aplikacji sieci web
Istnieje kilka zagadnień dotyczących uruchamianie aplikacji sieci web i zarządzanie planami usługi aplikacji w elemencie ASE, które należy wziąć pod uwagę toobe.  

Jak wspomniano wcześniej, właściciel hello hello ASE odpowiada dla rozmiaru hello hello systemu i w związku z tym są również odpowiedzialne za zapewnienie, że istnieje wystarczająca pojemność toohost hello potrzeby planów usługi aplikacji. Jeśli nie ma żadnych dostępnych pracowników, nie będzie można toocreate stanie planu usługi aplikacji.  Dotyczy to również true tooscaling zapasowej swojej aplikacji sieci web.  Jeśli potrzebujesz więcej wystąpień, konieczne będzie tooget Twojego środowiska usługi aplikacji admin tooadd więcej pracowników.

Po utworzeniu aplikacji sieci web i plan usługi aplikacji jest tooscale dobrze go.  W elemencie ASE należy zawsze toohave co najmniej 2 wystąpienia z odporności tooprovide planu usługi aplikacji — dla aplikacji.  Skalowanie usługi aplikacji — plan w elemencie ASE jest hello takie same jak zwykle za pośrednictwem hello planu usługi aplikacji interfejsu użytkownika.  Aby uzyskać więcej informacji na temat skalowania [jak tooscale aplikacji sieci web w środowisku usługi aplikacji](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
