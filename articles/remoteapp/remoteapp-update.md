---
title: "aaaUpdate kolekcji usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupdate kolekcji usługi Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Aktualizowanie kolekcji w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Dostarczane przez czas natychmiastową, gdy są potrzebne aplikacji hello tooupdate lub obrazu w kolekcji usługi Azure RemoteApp. Jeśli używasz obrazów hello uwzględnionych w subskrypcji usługi Azure RemoteApp w chmurowym lub hybrydowym kolekcji, wszystkie aktualizacje są obsługiwane przez usługi Azure RemoteApp, więc można umieścić łatwe.

Jeśli używasz niestandardowego obrazu (Aby zbudować od początku lub utworzonej przez zmodyfikowanie jeden z naszych obrazów) jest odpowiada za obsługę obrazu hello i aplikacji. Jeśli potrzebujesz tooupdate obrazu lub dowolną z aplikacji hello w nim, należy toocreate nowych, zaktualizowanych wersji hello obrazu, a następnie zastąp hello istniejącego obrazu w kolekcji z tego nowego zaktualizowanego obrazu.

Tak jak uzyskać o aktualizowaniu kolekcji? Jest bardzo prosta:

1. Obraz powitania aktualizacji używane w kolekcji. Zastosuj wszelkie poprawki lub wymagane aktualizacje, a następnie zapisz go z nową nazwą.
2. [Przekaż](remoteapp-uploadimage.md) lub [zaimportować](remoteapp-image-on-azurevm.md) tooRemoteApp tego obrazu.
3. Teraz, na stronie kolekcji powitania kliknij **aktualizacji**.
4. Wybierz nowy obraz powitania od hello **obrazu szablonu** listy.
5. Poniżej przedstawiono część trudnych hello — jak potrzebny toodecide toodeal z wszyscy użytkownicy, którzy aktualnie używają aplikacji hello kolekcji. Masz hello następujące opcje:
   
   * **Daj użytkownikom 60 minut po aktualizacji hello**. Natychmiast po zakończeniu aktualizacji hello Azure RemoteApp wyświetli komunikat tooany użytkownicy aktywni, informacją toosave ich pracy i dziennika Wyłącz i ponownie zalogować. Po 60 minutach aktywni użytkownicy, którzy nie logowali się poza zostaną automatycznie wylogowani. Użytkownicy mogą natychmiast zalogować ponownie.
   * **Wyloguj użytkowników natychmiast**. Natychmiast po zakończeniu aktualizacji hello Wyloguj wszystkich użytkowników automatycznie bez ostrzeżenia. Ta opcja może spowodować utratę danych przez użytkowników. One jednak natychmiast ponownie toohello aplikacji.
6. Kliknij przycisk Aktualizuj hello toostart znacznik wyboru hello.

