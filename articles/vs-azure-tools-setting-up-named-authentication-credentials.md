---
title: "aaaSetting się poświadczenia uwierzytelniania o nazwie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa w chmurze programu Visual Studio za pomocą tooauthenticate żądań tooAzure toopublish tooAzure aplikacji z programu Visual Studio lub toomonitor istniejących poświadczeń tootooprovide... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a>Konfigurowanie poświadczeń uwierzytelniania o nazwie
toopublish tooAzure aplikacji z programu Visual Studio lub toomonitor istniejącej usługi chmury, musisz podać poświadczenia programu Visual Studio za pomocą tooauthenticate żądań tooAzure. Istnieje kilka obszarów w programie Visual Studio, w którym można zalogować się tooprovide te poświadczenia. Na przykład z hello Eksploratora serwera, możesz otworzyć menu skrótów hello hello **Azure** węzeł i wybierz polecenie **połączyć tooMicrosoft subskrypcji platformy Azure...** . Po zalogowaniu, hello informacji o subskrypcji skojarzonych z Twoim kontem platformy Azure jest dostępna w programie Visual Studio i nie ma nic więcej masz toodo.

Narzędzia platformy Azure obsługuje również starsze sposób podawania poświadczeń, przy użyciu hello subskrypcji (plik .publishsettings). W tym temacie opisano metody nadal jest obsługiwany w 2.2 zestawu SDK platformy Azure.

Witaj, następujące elementy są wymagane dla tooAzure uwierzytelniania:

* Identyfikator subskrypcji
* Prawidłowy certyfikat X.509 v3

> [!NOTE]
> Hello długość klucza certyfikatu X.509 v3 hello musi wynosić co najmniej 2048 bitów. Azure spowoduje odrzucenie dowolny certyfikat, który nie spełnia tego wymagania lub nie jest prawidłowa.
>
>

Visual Studio będzie korzystać identyfikator subskrypcji oraz hello dane certyfikatu jako poświadczeń. odwołuje się hello subskrypcji (plik .publishsettings), który zawiera klucz publiczny certyfikatu hello Hello odpowiednie poświadczenia. Witaj subskrypcji plik może zawierać poświadczeń dla więcej niż jedną subskrypcję.

Można edytować hello informacji o subskrypcji z hello **subskrypcji nowy i edytować** okno dialogowe, zgodnie z objaśnieniem w dalszej części tego tematu.

Chcesz toocreate certyfikatu samodzielnie, mogą odwoływać się instrukcjami toohello [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) , a następnie ręcznie przekazać toohello certyfikatu hello [klasycznego portalu Azure ](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Te poświadczenia, które program Visual Studio wymaga toomanage, które nie są usługi w chmurze hello tych samych poświadczeń, które są wymagane tooauthenticate Żądanie hello usług magazynu platformy Azure.
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>Importuj, konfigurowanie lub edytowanie poświadczeń uwierzytelniania w programie Visual Studio
Można importować, skonfigurować lub zmodyfikować poświadczenia uwierzytelniania w hello **nową subskrypcję** okno dialogowe, które pojawia się po wykonaniu hello następujące działania:

* W **Eksploratora serwera**, otwórz menu skrótów hello hello **Azure** węzła, wybierz **zarządzanie i subskrypcje filtru...** , wybierz hello **certyfikaty** , a następnie wykonaj jedną z następujących hello:

    * Wybierz **zaimportować** dialogowe Importuj subskrypcji platformy Microsoft Azure hello tooopen której można pobrać pliku subskrypcje hello hello aktualnie załadowany subskrypcji, tooits przeglądania Lokalizacja pobierania, a następnie zaimportuj go do użycia w uwierzytelnianie.
    * Wybierz **nowy** tooopen hello nową subskrypcję okno, której można skonfigurować nowej subskrypcji do użytku podczas uwierzytelniania.
    * Wybierz **Edytuj** (po wybraniu subskrypcji active) tooopen: hello okna dialogowego Edytowanie subskrypcji którym można edytować istniejącą subskrypcję do użycia w przypadku uwierzytelniania. 

Witaj poniższej procedurze przyjęto, że hello **nową subskrypcję** jest otwarte okno dialogowe.

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a>tooset się poświadczenia uwierzytelniania w programie Visual Studio
1. W hello **wybierz istniejący certyfikat** dla listy uwierzytelniania należy wybrać certyfikat.
2. Wybierz hello **Kopiuj hello pełną ścieżkę** łącza. Ścieżka Hello hello certyfikatu (pliku cer) jest skopiowany toohello Schowka.

   > [!IMPORTANT]
   > toopublish aplikacji platformy Azure z programu Visual Studio, możesz przekazać ten toohello certyfikatu [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   >
   >
3. tooupload hello certyfikatu toohello portalu Azure:

   1. Otwórz hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   2. W przypadku wyświetlenia monitu zaloguj się w portalu toohello, a następnie przejdź zbyt**ustawienia**, **certyfikaty zarządzania**.
   3. W okienku certyfikatów zarządzania hello, wybierz **przekazać**.
   4. Wybierz subskrypcję platformy Azure, Wklej hello pełną ścieżkę pliku .cer hello, który został właśnie utworzony, a następnie wybierz **przekazać**.
