---
title: "tooAzure aaaConnect usług Analysis Services przy użyciu programu Excel | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooan Azure Analysis Services serwera przy użyciu programu Excel."
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="9948a-103">Łączenie z programem Excel</span><span class="sxs-lookup"><span data-stu-id="9948a-103">Connect with Excel</span></span>

<span data-ttu-id="9948a-104">Po utworzeniu serwera na platformie Azure i wdrożone tooit modelu tabelarycznego, wszystko gotowe tooconnect i rozpocząć eksplorowanie danych.</span><span class="sxs-lookup"><span data-stu-id="9948a-104">Once you've created a server in Azure, and deployed a tabular model tooit, you're ready tooconnect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="9948a-105">Łączenie programu Excel</span><span class="sxs-lookup"><span data-stu-id="9948a-105">Connect in Excel</span></span>

<span data-ttu-id="9948a-106">Podłączanie tooa serwera w programie Excel jest obsługiwana za pomocą pobieranie danych w programie Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="9948a-106">Connecting tooa server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="9948a-107">Łączenie za pomocą hello Kreator importu tabeli w dodatku Power Pivot nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="9948a-107">Connecting by using hello Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="9948a-108">**tooconnect w programie Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="9948a-108">**tooconnect in Excel 2016**</span></span>

1. <span data-ttu-id="9948a-109">W programie Excel 2016, na powitania **danych** wstążki, kliknij przycisk **Pobierz dane zewnętrzne** > **z innych źródeł** > **usług Analysis Services** .</span><span class="sxs-lookup"><span data-stu-id="9948a-109">In Excel 2016, on hello **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="9948a-110">W hello Kreator połączenia danych, w **nazwy serwera**, wprowadź nazwę serwera hello, łącznie z protokołem i identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="9948a-110">In hello Data Connection Wizard, in **Server name**, enter hello server name including protocol and URI.</span></span> <span data-ttu-id="9948a-111">Następnie w **poświadczeń logowania**, wybierz pozycję **hello użyj następującej nazwy użytkownika i hasła**, a następnie wpisz nazwę organizacji użytkownika hello, na przykład nancy@adventureworks.comi hasło.</span><span class="sxs-lookup"><span data-stu-id="9948a-111">Then, in **Logon credentials**, select **Use hello following User Name and Password**, and then type hello organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Nawiązywanie połączenia z logowania programu Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="9948a-113">W **wybierz bazę danych i tabeli**wybierz hello bazy danych i modelu lub perspektywy, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="9948a-113">In **Select Database and Table**, select hello database and model or perspective, and then click **Finish**.</span></span>
   
    ![Nawiązywanie połączenia z wybierz model programu Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="9948a-115">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9948a-115">See also</span></span>
<span data-ttu-id="9948a-116">[Biblioteki klienta](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="9948a-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="9948a-117">Zarządzanie serwerem</span><span class="sxs-lookup"><span data-stu-id="9948a-117">Manage your server</span></span>](analysis-services-manage.md)     


