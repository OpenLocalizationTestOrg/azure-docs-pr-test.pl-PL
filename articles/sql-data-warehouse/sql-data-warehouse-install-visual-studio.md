---
title: "aaaInstall programu Visual Studio i narzędzi SSDT dla usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Instalacja programu Visual Studio i narzędzi SQL Server Data Tools (SSDT) dla usługi Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>Instalacja programu Visual Studio i narzędzi SSDT dla usługi SQL Data Warehouse
toodevelop aplikacji dla usługi SQL Data Warehouse, zalecamy używanie hello najnowszej wersji programu Visual Studio z hello najnowszej wersji programu SQL Server Data Tools (SSDT).  W celu zapewnienia zgodności z poprzednimi wersjami możliwa jest również obsługa programu Visual Studio 2013 Update 5 z narzędziami SSDT.  

Za pomocą programu Visual Studio z narzędziami SSDT pozwala toouse hello Eksplorator obiektów SQL Server toovisually eksplorować tabele, widoki, procedury składowane i wiele innych obiektów w magazynie danych SQL, a także wykonywać zapytania.

> [!NOTE]
> Usługa SQL Data Warehouse jeszcze nie obsługuje projektów bazy danych programu Visual Studio.  Ta funkcja zostanie dodana w przyszłej wersji.
> 
> 

## <a name="step-1-install-visual-studio"></a>Krok 1: Zainstaluj program Visual Studio
Wykonaj te toodownload łącza, a następnie zainstalować program Visual Studio. Jeśli masz już programu Visual Studio 2013 lub nowszy, możesz pominąć tooStep 2, należy zainstalować narzędzia SSDT.

1. [Pobierz program Visual Studio][].
2. Wykonaj hello [Instalowanie programu Visual Studio] [ Installing Visual Studio] prowadzą w witrynie MSDN i wybierz hello domyślne konfiguracje.

## <a name="step-2-install-ssdt"></a>Krok 2: instalowanie narzędzi SSDT
tooinstall narzędzi SSDT dla programu Visual Studio po prostu Wyszukaj aktualizację SSDT z poziomu programu Visual Studio, wykonaj następujące czynności.

1. W programie Visual Studio kliknij **narzędzia** / **rozszerzenia i aktualizacje...** / **Aktualizacje**
2. Wybierz opcję **Aktualizacje produktu** i poszukaj **Microsoft SQL Server Update do oprzyrządowania bazy danych**

Jeśli aktualizacja nie zostanie znaleziona, powinien mieć zainstalowaną najnowszą wersję hello.  tooconfirm SSDT jest zainstalowany, kliknij **pomocy** / **Microsoft Visual Studio** i wyszukaj program SQL Server Data Tools na liście hello.  Witaj najnowszą wersję narzędzi SSDT to 14.0.60525.0.  Jeśli hello tooinstall opcja nie jest dostępna w programie Visual Studio, możesz też użytkownik może odwiedzić hello [pobieranie narzędzi SSDT] [ SSDT Download] strony toodownload i zainstalować narzędzia SSDT ręcznie.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz najnowszą wersję narzędzi SSDT hello wszystko będzie gotowe za[połączyć] [ connect] tooyour SQL Data Warehouse.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Pobierz program Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
