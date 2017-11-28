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
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="1d3a6-103">Instalacja programu Visual Studio i narzędzi SSDT dla usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1d3a6-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="1d3a6-104">toodevelop aplikacji dla usługi SQL Data Warehouse, zalecamy używanie hello najnowszej wersji programu Visual Studio z hello najnowszej wersji programu SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="1d3a6-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="1d3a6-105">W celu zapewnienia zgodności z poprzednimi wersjami możliwa jest również obsługa programu Visual Studio 2013 Update 5 z narzędziami SSDT.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="1d3a6-106">Za pomocą programu Visual Studio z narzędziami SSDT pozwala toouse hello Eksplorator obiektów SQL Server toovisually eksplorować tabele, widoki, procedury składowane i wiele innych obiektów w magazynie danych SQL, a także wykonywać zapytania.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="1d3a6-107">Usługa SQL Data Warehouse jeszcze nie obsługuje projektów bazy danych programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="1d3a6-108">Ta funkcja zostanie dodana w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="1d3a6-109">Krok 1: Zainstaluj program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d3a6-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="1d3a6-110">Wykonaj te toodownload łącza, a następnie zainstalować program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="1d3a6-111">Jeśli masz już programu Visual Studio 2013 lub nowszy, możesz pominąć tooStep 2, należy zainstalować narzędzia SSDT.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="1d3a6-112">[Pobierz program Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="1d3a6-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="1d3a6-113">Wykonaj hello [Instalowanie programu Visual Studio] [ Installing Visual Studio] prowadzą w witrynie MSDN i wybierz hello domyślne konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="1d3a6-114">Krok 2: instalowanie narzędzi SSDT</span><span class="sxs-lookup"><span data-stu-id="1d3a6-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="1d3a6-115">tooinstall narzędzi SSDT dla programu Visual Studio po prostu Wyszukaj aktualizację SSDT z poziomu programu Visual Studio, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="1d3a6-116">W programie Visual Studio kliknij **narzędzia** / **rozszerzenia i aktualizacje...**</span><span class="sxs-lookup"><span data-stu-id="1d3a6-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="1d3a6-117"> / **Aktualizacje**</span><span class="sxs-lookup"><span data-stu-id="1d3a6-117"> / **Updates**</span></span>
2. <span data-ttu-id="1d3a6-118">Wybierz opcję **Aktualizacje produktu** i poszukaj **Microsoft SQL Server Update do oprzyrządowania bazy danych**</span><span class="sxs-lookup"><span data-stu-id="1d3a6-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="1d3a6-119">Jeśli aktualizacja nie zostanie znaleziona, powinien mieć zainstalowaną najnowszą wersję hello.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="1d3a6-120">tooconfirm SSDT jest zainstalowany, kliknij **pomocy** / **Microsoft Visual Studio** i wyszukaj program SQL Server Data Tools na liście hello.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="1d3a6-121">Witaj najnowszą wersję narzędzi SSDT to 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="1d3a6-122">Jeśli hello tooinstall opcja nie jest dostępna w programie Visual Studio, możesz też użytkownik może odwiedzić hello [pobieranie narzędzi SSDT] [ SSDT Download] strony toodownload i zainstalować narzędzia SSDT ręcznie.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d3a6-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d3a6-123">Next steps</span></span>
<span data-ttu-id="1d3a6-124">Teraz, gdy masz najnowszą wersję narzędzi SSDT hello wszystko będzie gotowe za[połączyć] [ connect] tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1d3a6-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Pobierz program Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
