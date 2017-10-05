---
title: "Aktualizowanie kolekcji usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aktualizowanie kolekcji usługi Azure RemoteApp"
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
ms.openlocfilehash: 454d78445d6092aec9eaa383e4c50cf15195848c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Aktualizowanie kolekcji w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Dostarczane przez czas natychmiastową, gdy są potrzebne do aktualizacji aplikacji lub obrazu w kolekcji usługi Azure RemoteApp. Jeśli używasz jednego z obrazów zawartych w ramach subskrypcji usługi Azure RemoteApp w chmurowym lub hybrydowym kolekcji, wszystkie aktualizacje są obsługiwane przez usługi Azure RemoteApp, więc można umieścić łatwe.

Jeśli używasz niestandardowego obrazu (Aby zbudować od początku lub utworzonej przez zmodyfikowanie jeden z naszych obrazów) jest odpowiedzialny za obsługę obrazu i aplikacji. Musisz zaktualizować obrazu lub dowolną z aplikacji w nim, należy utworzyć nowych, zaktualizowanych wersji obrazu, a następnie zastąp istniejący obraz w kolekcji z tego nowego zaktualizowanego obrazu.

Tak jak uzyskać o aktualizowaniu kolekcji? Jest bardzo prosta:

1. Aktualizowanie obrazu, który został użyty w kolekcji. Zastosuj wszelkie poprawki lub wymagane aktualizacje, a następnie zapisz go z nową nazwą.
2. [Przekaż](remoteapp-uploadimage.md) lub [zaimportować](remoteapp-image-on-azurevm.md) obrazu do usługi RemoteApp.
3. Teraz, na stronie pobierania kliknij **aktualizacji**.
4. Wybierz nowy obraz z **obrazu szablonu** listy.
5. W tym miejscu jest wymagana - należy określić sposób postępowania w przypadku wszystkich użytkowników, którzy aktualnie używają aplikacji w kolekcji. Masz następujące opcje:
   
   * **Daj użytkownikom 60 minut po aktualizacji**. Natychmiast po zakończeniu aktualizacji usługi Azure RemoteApp zostanie wyświetlony komunikat do wszystkich aktywnych użytkowników informacją o zapisanie pracy i wylogowanie i ponowne zalogowanie. Po 60 minutach aktywni użytkownicy, którzy nie logowali się poza zostaną automatycznie wylogowani. Użytkownicy mogą natychmiast zalogować ponownie.
   * **Wyloguj użytkowników natychmiast**. Natychmiast po zakończeniu aktualizacji Wyloguj wszystkich użytkowników automatycznie bez ostrzeżenia. Ta opcja może spowodować utratę danych przez użytkowników. Jednak można ponownym połączeniu aplikacji natychmiast.
6. Kliknij znacznik wyboru, aby rozpocząć aktualizację.

