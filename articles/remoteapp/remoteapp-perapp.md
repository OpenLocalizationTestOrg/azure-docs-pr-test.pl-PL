---
title: "aaaPublish aplikacji tooindividual użytkowników w kolekcji usługi Azure RemoteApp (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak opublikować aplikacje tooindividual użytkowników, a nie w zależności od grup w usłudze Azure RemoteApp."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>Publikowanie aplikacji tooindividual użytkowników w kolekcji usługi Azure RemoteApp (wersja zapoznawcza)
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

W tym artykule opisano sposób toopublish aplikacji tooindividual użytkowników w kolekcji usługi Azure RemoteApp. To jest nowa funkcja w usłudze Azure RemoteApp, obecnie w prywatnej wersji zapoznawczej i dostępne tooselect tylko pierwszych użytkowników do celów oceny.

Pierwotnie usługa Azure RemoteApp obsługiwała tylko jeden sposób publikowania aplikacji: hello administrator publikował aplikacje z obrazu hello i będą one widoczne tooall użytkowników w kolekcji hello.

Typowy scenariusz obejmuje tooinclude wiele aplikacji w jednej obrazu i wdrożenie jednej kolekcji w kolejności tooreduce zarządzania kosztów. Często nie wszystkie aplikacje są odpowiednie tooall użytkowników — Administratorzy woleliby toopublish aplikacji tooindividual użytkowników, aby nie były widoczne zbędne aplikacje w źródle aplikacji.

Ta funkcja jest już dostępna w usłudze Azure RemoteApp, obecnie jako ograniczona funkcja wersji zapoznawczej. Oto krótkie podsumowanie nowej funkcji hello:

1. Kolekcję można ustawić w jeden z dwóch trybów:
   
   * Hello oryginalny tryb kolekcji, gdzie wszyscy użytkownicy kolekcji widzą wszystkie opublikowane aplikacje. Jest to tryb domyślny hello.
   * Witaj nowy tryb aplikacji, którym użytkownicy widzą tylko aplikacje, które zostały jawnie przypisane toothem
2. W momencie hello tryb aplikacji hello można włączyć tylko przy użyciu poleceń cmdlet środowiska PowerShell usługi Azure RemoteApp.
   
   * Gdy Ustaw tryb tooapplication, przypisanie użytkownika w kolekcji hello nie mogą być zarządzane za pośrednictwem hello portalu Azure. Przypisanie użytkownika musi toobe zarządzanych za pomocą poleceń cmdlet programu PowerShell.
3. Użytkownicy widzą tylko aplikacje hello bezpośrednio opublikowane toothem. Jednak może nadal być możliwe do toolaunch użytkownika hello inne aplikacje, które są dostępne w obrazie hello uzyskując dostęp do nich bezpośrednio w systemie operacyjnym hello.
   
   * Ta funkcja nie zapewnia bezpiecznej blokady aplikacji; lecz tylko ogranicza ich widoczność w źródle aplikacji hello.
   * Użytkownicy tooisolate z aplikacji, należy należy toouse oddzielne kolekcje dla tej.

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>Jak tooget poleceń cmdlet środowiska PowerShell usługi Azure RemoteApp
tootry hello nowych wersji zapoznawczej funkcji, należy poleceń cmdlet programu Azure PowerShell toouse. Obecnie nie jest możliwe toouse hello Azure Management portal tooenable hello nowego trybu publikowania aplikacji.

Najpierw upewnij się, że masz hello [modułu Azure PowerShell](/powershell/azure/overview) zainstalowane.

Następnie uruchom konsolę programu PowerShell hello w trybie administratora i hello uruchom następujące polecenia cmdlet:

        Add-AzureAccount

Może zostać wyświetlony monit o podanie nazwy użytkownika i hasła platformy Azure. Po zalogowaniu można poleceń cmdlet usługi Azure RemoteApp stanie toorun względem subskrypcji platformy Azure.

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>Jak toocheck trybu kolekcji jest w
Uruchom następujące polecenia cmdlet hello:

        Get-AzureRemoteAppCollection <collectionName>

![Tryb kolekcji hello wyboru](./media/remoteapp-perapp/araacllelvel.png)

Witaj właściwość AclLevel może mieć hello następujące wartości:

* Kolekcja: hello oryginalny Tryb publikowania. Wszyscy użytkownicy widzą wszystkie opublikowane aplikacje.
* : Hello nowego trybu publikowania aplikacji. Użytkownicy widzą tylko hello aplikacje opublikowane bezpośrednio toothem.

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>Jak tryb publikowania tooapplication tooswitch
Uruchom następujące polecenia cmdlet hello:

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

Stan publikowania aplikacji zostanie zachowany: początkowo wszyscy użytkownicy będą widzieli wszystkie oryginalnie opublikowane aplikacje hello.

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>Jak toolist użytkowników, którzy mogą przeglądać określonej aplikacji
Uruchom następujące polecenia cmdlet hello:

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Ta lista zawiera wszystkich użytkowników, którzy mogą przeglądać aplikacji hello.

Uwaga: Można wyświetlić aliasy aplikacji hello (o nazwie "app alias" w powyższej składni hello) systemem Get AzureRemoteAppProgram - CollectionName <collectionName>.

## <a name="how-tooassign-an-application-tooa-user"></a>Jak tooassign użytkownika tooa aplikacji
Uruchom następujące polecenia cmdlet hello:

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

Hello użytkownik zobaczy aplikacji hello w kliencie usługi Azure RemoteApp hello i będą mogli tooconnect tooit.

## <a name="how-tooremove-an-application-from-a-user"></a>Jak tooremove aplikacji przez użytkownika
Uruchom następujące polecenia cmdlet hello:

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Przekazywanie opinii
Dziękujemy za Twoje opinie i sugestie dotyczące tej funkcji wersji zapoznawczej. Wypełnij hello [ankiety](http://www.instant.ly/s/FDdrb) toolet nam poznać Twoje zdanie.

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>Nie mam funkcja w wersji zapoznawczej hello tootry szansy?
Jeśli nie korzystasz w wersji zapoznawczej hello jeszcze, użyj tej [ankiety](http://www.instant.ly/s/AY83p) toorequest dostępu.

