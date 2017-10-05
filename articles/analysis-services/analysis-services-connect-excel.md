---
title: "Połącz do usług Azure Analysis Services przy użyciu programu Excel | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak połączyć się z serwerem usług Analysis Services dla platformy Azure przy użyciu programu Excel."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: d51b6980120f1cf9bc8d053d463a73ac600b915f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="2a364-103">Łączenie z programem Excel</span><span class="sxs-lookup"><span data-stu-id="2a364-103">Connect with Excel</span></span>

<span data-ttu-id="2a364-104">Po utworzeniu serwera na platformie Azure i wdrożone modelu tabelarycznego, możesz przystąpić do łączenia i rozpocząć eksplorowanie danych.</span><span class="sxs-lookup"><span data-stu-id="2a364-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="2a364-105">Łączenie programu Excel</span><span class="sxs-lookup"><span data-stu-id="2a364-105">Connect in Excel</span></span>

<span data-ttu-id="2a364-106">Łączenie z serwerem w programie Excel jest obsługiwana przy użyciu pobieranie danych w programie Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="2a364-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="2a364-107">Łączenie za pomocą Kreatora importu tabeli w dodatku Power Pivot nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2a364-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="2a364-108">**Aby połączyć w programie Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="2a364-108">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="2a364-109">W programie Excel 2016, w **danych** wstążki, kliknij przycisk **Pobierz dane zewnętrzne** > **z innych źródeł** > **usług Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="2a364-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="2a364-110">W Kreatorze połączenia danych w **nazwy serwera**, wprowadź nazwę serwera, łącznie z protokołem i identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="2a364-110">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span></span> <span data-ttu-id="2a364-111">Następnie w **poświadczeń logowania**, wybierz pozycję **poniższe nazwy użytkownika i hasła**, a następnie wpisz nazwę organizacji użytkownika, na przykład nancy@adventureworks.comi hasło.</span><span class="sxs-lookup"><span data-stu-id="2a364-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Nawiązywanie połączenia z logowania programu Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="2a364-113">W **wybierz bazę danych i tabeli**, wybierz bazę danych i modelu lub perspektywy, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2a364-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Nawiązywanie połączenia z wybierz model programu Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="2a364-115">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2a364-115">See also</span></span>
<span data-ttu-id="2a364-116">[Biblioteki klienta](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="2a364-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="2a364-117">Zarządzanie serwerem</span><span class="sxs-lookup"><span data-stu-id="2a364-117">Manage your server</span></span>](analysis-services-manage.md)     


