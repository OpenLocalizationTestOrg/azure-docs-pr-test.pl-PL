---
title: "aaaSchemas dla sprawdzanie poprawności kodu XML - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdzanie poprawności dokumentów XML za pomocą schematów dla usługi Azure Logic Apps i pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="e3ff5-103">Walidacja danych XML o schematach dla usługi Azure Logic Apps i hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="e3ff5-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="e3ff5-104">Schematy potwierdzić, że dokumenty XML hello otrzymany są prawidłowe i hello oczekiwać dane w formacie wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="e3ff5-105">Schematy również pomóc sprawdzania poprawności komunikatów, które są wymieniane w scenariuszu B2B.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="e3ff5-106">Dodawanie schematu</span><span class="sxs-lookup"><span data-stu-id="e3ff5-106">Add a schema</span></span>

1. <span data-ttu-id="e3ff5-107">Hello portalu Azure, wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-107">In hello Azure portal, select **More services**.</span></span>

    ![Portalu Azure, "Więcej usług"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="e3ff5-109">W polu wyszukiwania filtr hello, wprowadź **integracji**i wybierz **konta integracji** z listy wyników hello.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![Pole wyszukiwania filtru](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="e3ff5-111">Wybierz hello **konta integracji** miejscu tooadd hello schematu.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![Lista kont integracji](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="e3ff5-113">Wybierz hello **schematy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-113">Choose hello **Schemas** tile.</span></span>

    ![Przykład integracji konta, "Schematy"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="e3ff5-115">Dodaj plik schematu mniejszy niż 2 MB</span><span class="sxs-lookup"><span data-stu-id="e3ff5-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="e3ff5-116">W hello **schematy** bloku, który zostanie otwarty (od hello poprzednich krokach), wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![Schematy bloku "Dodaj"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="e3ff5-118">Wprowadź nazwę schematu.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-118">Enter a name for your schema.</span></span> <span data-ttu-id="e3ff5-119">Przekaż plik schematu hello wybierając hello folderu ikona dalej toohello **schematu** pole.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="e3ff5-120">Po zakończeniu procesu przekazywania hello wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-120">After hello upload process completes, select **OK**.</span></span>

    ![Zrzut ekranu przedstawiający "Dodaj Schema", z wyróżnioną pozycją "mały plik"](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="e3ff5-122">Dodaj plik schematu większych niż 2 MB (up too8 maksymalnie MB)</span><span class="sxs-lookup"><span data-stu-id="e3ff5-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="e3ff5-123">Te kroki się różnić w zależności na poziomie dostępu do kontenera obiektów blob hello: **publicznego** lub **dostępu anonimowego**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="e3ff5-124">**toodetermine ten poziom dostępu**</span><span class="sxs-lookup"><span data-stu-id="e3ff5-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="e3ff5-125">Otwórz **Eksploratora usługi Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="e3ff5-126">W obszarze **kontenerów obiektów Blob**, wybierz kontener obiektów blob hello ma.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="e3ff5-127">Wybierz **zabezpieczeń**, **poziom dostępu**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="e3ff5-128">Jeśli poziom dostępu zabezpieczeń obiektu blob hello jest **publicznych**, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-128">If hello blob security access level is **Public**, follow these steps.</span></span>

![Azure Eksploratora usługi Storage, "Kontenerów obiektów Blob", "Zabezpieczenia" i "Public" wyróżnione](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="e3ff5-130">Przekaż konta magazynu tooyour schematu hello i skopiuj hello identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![Konto magazynu o identyfikatorze URI wyróżnione](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="e3ff5-132">W **Dodaj schemat**, wybierz pozycję **plików o dużym**i podaj hello identyfikatora URI w hello **URI zawartości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    ![Schematy przycisk "Dodaj" i "Dużych plików" wyróżnione](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="e3ff5-134">Jeśli poziom dostępu zabezpieczeń obiektu blob hello jest **dostępu anonimowego**, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

![Azure Eksploratora usługi Storage, "Kontenerów obiektów Blob", "Zabezpieczenia" i "Brak dostępu anonimowego" wyróżnione](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="e3ff5-136">Przekaż konta magazynu tooyour schematu hello.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-136">Upload hello schema tooyour storage account.</span></span>

    ![Konto magazynu](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="e3ff5-138">Generowanie sygnatury dostępu współdzielonego dla hello schematu.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-138">Generate a shared access signature for hello schema.</span></span>

    ![Konto magazynu z wyróżnionym kartę sygnatur dostępu współdzielonego](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="e3ff5-140">W **Dodaj schemat**, wybierz pozycję **plików o dużym**i podaj identyfikator URI sygnatury dostępu współdzielonego hello w hello **URI zawartości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    ![Schematy przycisk "Dodaj" i "Dużych plików" wyróżnione](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="e3ff5-142">W hello **schematy** blok konta integracji, nowo dodanego schemat powinien zostać wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Konta integracji z "Schematy" i hello wyróżnione nowego schematu.](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="e3ff5-144">Edytuj schematów</span><span class="sxs-lookup"><span data-stu-id="e3ff5-144">Edit schemas</span></span>

1. <span data-ttu-id="e3ff5-145">Wybierz hello **schematy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="e3ff5-146">Po hello **schematy** zostanie otwarty blok, wybierz hello schematu, które mają tooedit.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="e3ff5-147">Na powitania **schematy** bloku, wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![Schematy bloku](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="e3ff5-149">Plik schematu hello wybierz, czy tooedit, a następnie wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![Otwórz schematu pliku tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="e3ff5-151">Azure wskazuje a wiadomość hello schemat został pomyślnie przekazany.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="e3ff5-152">Usuwanie schematów</span><span class="sxs-lookup"><span data-stu-id="e3ff5-152">Delete schemas</span></span>

1. <span data-ttu-id="e3ff5-153">Wybierz hello **schematy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="e3ff5-154">Po hello **schematy** zostanie otwarty blok, wybierz hello schematu ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="e3ff5-155">Na powitania **schematy** bloku, wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![Schematy bloku](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="e3ff5-157">Wybierz pozycję tooconfirm, które mają toodelete hello wybrany schemat **tak**.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    ![Komunikat potwierdzający "Schematu delete"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="e3ff5-159">W hello **schematy** bloku hello schematu listy odświeża i nie zawiera już hello schematu, który zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="e3ff5-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    ![Twoje konto, z wyróżnioną pozycją "schematy" integracji](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="e3ff5-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3ff5-161">Next steps</span></span>
* <span data-ttu-id="e3ff5-162">[Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw hello").</span><span class="sxs-lookup"><span data-stu-id="e3ff5-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

