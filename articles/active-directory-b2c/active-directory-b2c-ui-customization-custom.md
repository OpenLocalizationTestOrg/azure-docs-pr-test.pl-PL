---
title: "Dostosowywanie interfejsu użytkownika za pomocą niestandardowych zasad — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat dostosowywania interfejsu użytkownika (UI), gdy użycie zasad niestandardowych w usłudze Azure AD B2C."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: d5a3c0a323b31696d39e3d2b36317dec3a2337d7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="ff322-103">Usługa Azure Active Directory B2C: Konfigurowanie dostosowywania interfejsu użytkownika w zasadach niestandardowych</span><span class="sxs-lookup"><span data-stu-id="ff322-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ff322-104">Po zakończeniu pracy w tym artykule, konieczne będzie rejestracji i logowania zasady niestandardowe marki i wyglądu.</span><span class="sxs-lookup"><span data-stu-id="ff322-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="ff322-105">Z usługi Azure Active Directory B2C (Azure AD B2C), możesz uzyskać prawie pełną kontrolę nad zawartość HTML i CSS, które są prezentowane użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="ff322-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of the HTML and CSS content that's presented to users.</span></span> <span data-ttu-id="ff322-106">Użycie zasad niestandardowych, należy skonfigurować dostosowywania interfejsu użytkownika w XML, zamiast za pomocą formantów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ff322-106">When you use a custom policy, you configure UI customization in XML instead of using controls in the Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ff322-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ff322-107">Prerequisites</span></span>

<span data-ttu-id="ff322-108">Przed rozpoczęciem należy wykonać [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ff322-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="ff322-109">Powinien mieć pracy niestandardowych zasad rejestracji i logowania z kontami lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="ff322-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="ff322-110">Dostosowywanie interfejsu użytkownika strony</span><span class="sxs-lookup"><span data-stu-id="ff322-110">Page UI customization</span></span>

<span data-ttu-id="ff322-111">Za pomocą funkcji dostosowywania interfejsu użytkownika strony, można dostosować wygląd i działanie dowolne zasady niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="ff322-111">By using the page UI customization feature, you can customize the look and feel of any custom policy.</span></span> <span data-ttu-id="ff322-112">Można również utrzymać marki i wizualne spójności między aplikacji i usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ff322-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="ff322-113">Oto jak to działa: usługi Azure AD B2C kod w przeglądarce klienta, korzysta z podejścia nowoczesnych o nazwie [udostępniania zasobów między źródłami (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="ff322-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="ff322-114">Najpierw należy określić adres URL w zasadach niestandardowych z dostosowana zawartość HTML.</span><span class="sxs-lookup"><span data-stu-id="ff322-114">First, you specify a URL in the custom policy with customized HTML content.</span></span> <span data-ttu-id="ff322-115">Usługa Azure AD B2C scala elementy interfejsu użytkownika z zawartość HTML, który jest ładowany z danego adresu URL, a następnie wyświetla strony do klienta.</span><span class="sxs-lookup"><span data-stu-id="ff322-115">Azure AD B2C merges UI elements with the HTML content that's loaded from your URL and then displays the page to the customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="ff322-116">Tworzenie sieci HTML5 zawartości</span><span class="sxs-lookup"><span data-stu-id="ff322-116">Create your HTML5 content</span></span>

<span data-ttu-id="ff322-117">Tworzenie zawartości o nazwie markę produktu HTML w tytule.</span><span class="sxs-lookup"><span data-stu-id="ff322-117">Create HTML content with your product's brand name in the title.</span></span>

1. <span data-ttu-id="ff322-118">Skopiuj poniższy fragment kodu HTML.</span><span class="sxs-lookup"><span data-stu-id="ff322-118">Copy the following HTML snippet.</span></span> <span data-ttu-id="ff322-119">Jest poprawnie sformułowanym HTML5 z pustego elementu o nazwie  *\<div id = "interfejsu api"\>\</DIV\>*  znajdujących się w granicach  *\<treści\>*  tagów.</span><span class="sxs-lookup"><span data-stu-id="ff322-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within the *\<body\>* tags.</span></span> <span data-ttu-id="ff322-120">Ten element wskazuje, gdzie jest zawartość usługi Azure AD B2C do wstawienia.</span><span class="sxs-lookup"><span data-stu-id="ff322-120">This element indicates where Azure AD B2C content is to be inserted.</span></span>

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   ><span data-ttu-id="ff322-121">Ze względów bezpieczeństwa użycie JavaScript jest obecnie zablokowany do dostosowania.</span><span class="sxs-lookup"><span data-stu-id="ff322-121">For security reasons, the use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="ff322-122">Wklej skopiowane fragment kodu w edytorze tekstu, a następnie zapisz plik jako *dostosować ui.html*.</span><span class="sxs-lookup"><span data-stu-id="ff322-122">Paste the copied snippet in a text editor, and then save the file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="ff322-123">Tworzenie konta magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ff322-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="ff322-124">W tym artykule używamy magazynu obiektów Blob platformy Azure do hostowania zawartość.</span><span class="sxs-lookup"><span data-stu-id="ff322-124">In this article, we use Azure Blob storage to host our content.</span></span> <span data-ttu-id="ff322-125">Użytkownik może udostępnić zawartość na serwerze sieci web, ale należy [włączenia CORS na serwerze sieci web](https://enable-cors.org/server.html).</span><span class="sxs-lookup"><span data-stu-id="ff322-125">You can choose to host your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="ff322-126">Aby hostować tę zawartość HTML w magazynie obiektów Blob, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff322-126">To host this HTML content in Blob storage, do the following:</span></span>

1. <span data-ttu-id="ff322-127">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff322-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ff322-128">Na **Centrum** menu, wybierz opcję **nowy** > **magazynu** > **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="ff322-128">On the **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="ff322-129">Wprowadź unikatową **nazwa** dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff322-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="ff322-130">**Model wdrażania** może pozostawać **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="ff322-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="ff322-131">Zmień **rodzaj konta** do **magazynu obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="ff322-131">Change **Account Kind** to **Blob storage**.</span></span>
6. <span data-ttu-id="ff322-132">**Wydajność** może pozostawać **standardowe**.</span><span class="sxs-lookup"><span data-stu-id="ff322-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="ff322-133">**Replikacja** może pozostawać **RA-GRS**.</span><span class="sxs-lookup"><span data-stu-id="ff322-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="ff322-134">**Warstwa dostępu** może pozostawać **gorąca**.</span><span class="sxs-lookup"><span data-stu-id="ff322-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="ff322-135">**Szyfrowanie usługi Magazyn** może pozostawać **wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="ff322-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="ff322-136">Wybierz **subskrypcji** dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff322-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="ff322-137">Utwórz **grupy zasobów** lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="ff322-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="ff322-138">Wybierz **lokalizacji geograficznej** dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff322-138">Select the **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="ff322-139">Kliknij pozycję **Utwórz**, aby utworzyć konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff322-139">Click **Create** to create the storage account.</span></span>  
    <span data-ttu-id="ff322-140">Po zakończeniu wdrożenia **konta magazynu** automatycznie zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="ff322-140">After the deployment is completed, the **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="ff322-141">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="ff322-141">Create a container</span></span>

<span data-ttu-id="ff322-142">Aby utworzyć publicznego kontenera w magazynie obiektów Blob, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff322-142">To create a public container in Blob storage, do the following:</span></span>

1. <span data-ttu-id="ff322-143">Kliknij przycisk **omówienie** kartę.</span><span class="sxs-lookup"><span data-stu-id="ff322-143">Click the **Overview** tab.</span></span>
2. <span data-ttu-id="ff322-144">Kliknij przycisk **kontenera**.</span><span class="sxs-lookup"><span data-stu-id="ff322-144">Click **Container**.</span></span>
3. <span data-ttu-id="ff322-145">Aby uzyskać **nazwa**, typ **$root**.</span><span class="sxs-lookup"><span data-stu-id="ff322-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="ff322-146">Ustaw **dostęp typu** do **obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="ff322-146">Set **Access type** to **Blob**.</span></span>
5. <span data-ttu-id="ff322-147">Kliknij przycisk **$root** można otworzyć nowego kontenera.</span><span class="sxs-lookup"><span data-stu-id="ff322-147">Click **$root** to open the new container.</span></span>
6. <span data-ttu-id="ff322-148">Kliknij pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="ff322-148">Click **Upload**.</span></span>
7. <span data-ttu-id="ff322-149">Kliknij ikonę folderu **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="ff322-149">Click the folder icon next to **Select a file**.</span></span>
8. <span data-ttu-id="ff322-150">Przejdź do **dostosować ui.html**, który został wcześniej utworzony w [dostosowywania interfejsu użytkownika strony](#the-page-ui-customization-feature) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ff322-150">Go to **customize-ui.html**, which you created earlier in the [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="ff322-151">Kliknij pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="ff322-151">Click **Upload**.</span></span>
10. <span data-ttu-id="ff322-152">Wybierz ui.html Dostosowywanie obiektów blob, który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="ff322-152">Select the customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="ff322-153">Obok pozycji **adres URL**, kliknij przycisk **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="ff322-153">Next to **URL**, click **Copy**.</span></span>
12. <span data-ttu-id="ff322-154">W przeglądarce Wklej skopiowany adres URL, a następnie przejdź do witryny.</span><span class="sxs-lookup"><span data-stu-id="ff322-154">In a browser, paste the copied URL, and go to the site.</span></span> <span data-ttu-id="ff322-155">Jeśli witryna jest niedostępny, upewnij się, że typ dostępu do kontenera ustawiono **obiektu blob**.</span><span class="sxs-lookup"><span data-stu-id="ff322-155">If the site is inaccessible, make sure the container access type is set to **blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="ff322-156">Konfigurowanie mechanizmu CORS</span><span class="sxs-lookup"><span data-stu-id="ff322-156">Configure CORS</span></span>

<span data-ttu-id="ff322-157">Konfigurowanie magazynu obiektów Blob do udostępniania zasobów między źródłami w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ff322-157">Configure Blob storage for Cross-Origin Resource Sharing by doing the following:</span></span>

>[!NOTE]
><span data-ttu-id="ff322-158">Czy chcesz wypróbować dostosowywanie funkcji interfejsu użytkownika za pomocą naszej próbki kodu HTML i CSS zawartości?</span><span class="sxs-lookup"><span data-stu-id="ff322-158">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="ff322-159">Przygotowaliśmy [Narzędzie Pomocnik proste](active-directory-b2c-reference-ui-customization-helper-tool.md) który przekazuje i konfiguruje zawartość przykładowej na koncie magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="ff322-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="ff322-160">Jeśli używasz narzędzia, przejdź do [zmodyfikować zasady niestandardowe rejestracji i logowania](#modify-your-sign-up-or-sign-in-custom-policy).</span><span class="sxs-lookup"><span data-stu-id="ff322-160">If you use the tool, skip ahead to [Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="ff322-161">Na **magazynu** bloku, w obszarze **ustawienia**, otwórz **CORS**.</span><span class="sxs-lookup"><span data-stu-id="ff322-161">On the **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="ff322-162">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ff322-162">Click **Add**.</span></span>
3. <span data-ttu-id="ff322-163">Aby uzyskać **dozwolone źródła**, wpisz znak gwiazdki (\*).</span><span class="sxs-lookup"><span data-stu-id="ff322-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="ff322-164">W **dozwolonych zleceń** listy rozwijanej, wybierz **UZYSKAĆ** i **opcje**.</span><span class="sxs-lookup"><span data-stu-id="ff322-164">In the **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="ff322-165">Aby uzyskać **dozwolone nagłówki**, wpisz znak gwiazdki (\*).</span><span class="sxs-lookup"><span data-stu-id="ff322-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="ff322-166">Aby uzyskać **widoczne nagłówki**, wpisz znak gwiazdki (\*).</span><span class="sxs-lookup"><span data-stu-id="ff322-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="ff322-167">Aby uzyskać **maksymalny wiek (w sekundach)**, typ **200**.</span><span class="sxs-lookup"><span data-stu-id="ff322-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="ff322-168">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ff322-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="ff322-169">Test CORS</span><span class="sxs-lookup"><span data-stu-id="ff322-169">Test CORS</span></span>

<span data-ttu-id="ff322-170">Sprawdź, czy wszystko jest gotowe, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff322-170">Validate that you're ready by doing the following:</span></span>

1. <span data-ttu-id="ff322-171">Przejdź do [cors.org testu](http://test-cors.org/) witryny sieci Web, a następnie wklej adres URL w **zdalnego adresu URL** pole.</span><span class="sxs-lookup"><span data-stu-id="ff322-171">Go to the [test-cors.org](http://test-cors.org/) website, and then paste the URL in the **Remote URL** box.</span></span>
2. <span data-ttu-id="ff322-172">Kliknij przycisk **wysłać żądania**.</span><span class="sxs-lookup"><span data-stu-id="ff322-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="ff322-173">Jeśli wystąpi błąd, upewnij się, że Twoje [ustawień specyfikacji CORS](#configure-cors) są poprawne.</span><span class="sxs-lookup"><span data-stu-id="ff322-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="ff322-174">Może być również konieczne Wyczyść pamięć podręczną przeglądarki lub otworzyć sesji przeglądania w trybie prywatnym, naciskając klawisze Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="ff322-174">You might also need to clear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="ff322-175">Modyfikowanie zasad niestandardowych rejestracji i logowania</span><span class="sxs-lookup"><span data-stu-id="ff322-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="ff322-176">Najwyższego poziomu  *\<TrustFrameworkPolicy\>*  tagu, należy odnaleźć  *\<BuildingBlocks\>*  tagu.</span><span class="sxs-lookup"><span data-stu-id="ff322-176">Under the top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="ff322-177">W ramach  *\<BuildingBlocks\>*  Dodaj tagi,  *\<ContentDefinitions\>*  tag przez skopiowanie w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ff322-177">Within the *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying the following example.</span></span> <span data-ttu-id="ff322-178">Zastąp *your_storage_account* z nazwą konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff322-178">Replace *your_storage_account* with the name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="ff322-179">Przekaż zaktualizowany zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="ff322-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="ff322-180">W [portalu Azure](https://portal.azure.com), [przełącznika w kontekście dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), a następnie otwórz **usługi Azure AD B2C** bloku.</span><span class="sxs-lookup"><span data-stu-id="ff322-180">In the [Azure portal](https://portal.azure.com), [switch into the context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open the **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="ff322-181">Kliknij przycisk **wszystkich zasad**.</span><span class="sxs-lookup"><span data-stu-id="ff322-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="ff322-182">Kliknij przycisk **przekazywać zasady**.</span><span class="sxs-lookup"><span data-stu-id="ff322-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="ff322-183">Przekaż `SignUpOrSignin.xml` z  *\<ContentDefinitions\>*  tag, który wcześniej został dodany.</span><span class="sxs-lookup"><span data-stu-id="ff322-183">Upload `SignUpOrSignin.xml` with the *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="ff322-184">Testowanie zasad niestandardowych przy użyciu **Uruchom teraz**</span><span class="sxs-lookup"><span data-stu-id="ff322-184">Test the custom policy by using **Run now**</span></span>

1. <span data-ttu-id="ff322-185">Na **usługi Azure AD B2C** bloku, przejdź do **wszystkie zasady**.</span><span class="sxs-lookup"><span data-stu-id="ff322-185">On the **Azure AD B2C** blade, go to **All polices**.</span></span>
2. <span data-ttu-id="ff322-186">Wybierz zasady niestandardowe przekazywane i kliknij przycisk **Uruchom teraz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff322-186">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="ff322-187">Należy zalogowanie przy użyciu adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="ff322-187">You should be able to sign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="ff322-188">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="ff322-188">Reference</span></span>

<span data-ttu-id="ff322-189">Przykładowe szablonów można znaleźć do dostosowania interfejsu użytkownika w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="ff322-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="ff322-190">Folder sample_templates/wingtip zawiera następujące pliki HTML:</span><span class="sxs-lookup"><span data-stu-id="ff322-190">The sample_templates/wingtip folder contains the following HTML files:</span></span>

| <span data-ttu-id="ff322-191">Szablon HTML5</span><span class="sxs-lookup"><span data-stu-id="ff322-191">HTML5 template</span></span> | <span data-ttu-id="ff322-192">Opis</span><span class="sxs-lookup"><span data-stu-id="ff322-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="ff322-193">*phonefactor.HTML*</span><span class="sxs-lookup"><span data-stu-id="ff322-193">*phonefactor.html*</span></span> | <span data-ttu-id="ff322-194">Użyj tego pliku jako szablonu dla strony uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="ff322-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="ff322-195">*ResetPassword.HTML*</span><span class="sxs-lookup"><span data-stu-id="ff322-195">*resetpassword.html*</span></span> | <span data-ttu-id="ff322-196">Użyj tego pliku jako szablonu dla nie pamiętasz hasła strony.</span><span class="sxs-lookup"><span data-stu-id="ff322-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="ff322-197">*selfasserted.HTML*</span><span class="sxs-lookup"><span data-stu-id="ff322-197">*selfasserted.html*</span></span> | <span data-ttu-id="ff322-198">Użyj tego pliku jako szablonu dla kont społecznościowych stronę tworzenia konta, stronę tworzenia konta lokalnego konta lub stronę logowania konta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="ff322-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="ff322-199">*Unified.HTML*</span><span class="sxs-lookup"><span data-stu-id="ff322-199">*unified.html*</span></span> | <span data-ttu-id="ff322-200">Użyj tego pliku jako szablonu ujednoliconego strony rejestracji lub logowania.</span><span class="sxs-lookup"><span data-stu-id="ff322-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="ff322-201">*updateprofile.HTML*</span><span class="sxs-lookup"><span data-stu-id="ff322-201">*updateprofile.html*</span></span> | <span data-ttu-id="ff322-202">Użyj tego pliku jako szablonu strony aktualizacji profilu.</span><span class="sxs-lookup"><span data-stu-id="ff322-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="ff322-203">W [zmodyfikować sekcji rejestracji i logowania zasady niestandardowe](#modify-your-sign-up-or-sign-in-custom-policy), skonfigurowany zawartości definicji `api.idpselections`.</span><span class="sxs-lookup"><span data-stu-id="ff322-203">In the [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured the content definition for `api.idpselections`.</span></span> <span data-ttu-id="ff322-204">Pełny zestaw zawartości identyfikatorów definicji, które są rozpoznawane w ramach obsługi tożsamości usługi Azure AD B2C i ich opisy znajdują się w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="ff322-204">The full set of content definition IDs that are recognized by the Azure AD B2C identity experience framework and their descriptions are in the following table:</span></span>

| <span data-ttu-id="ff322-205">Identyfikator definicji zawartości</span><span class="sxs-lookup"><span data-stu-id="ff322-205">Content definition ID</span></span> | <span data-ttu-id="ff322-206">Opis</span><span class="sxs-lookup"><span data-stu-id="ff322-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="ff322-207">*API.error*</span><span class="sxs-lookup"><span data-stu-id="ff322-207">*api.error*</span></span> | <span data-ttu-id="ff322-208">**Strona błędu**.</span><span class="sxs-lookup"><span data-stu-id="ff322-208">**Error page**.</span></span> <span data-ttu-id="ff322-209">Ta strona jest wyświetlana po napotkaniu wyjątku lub wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="ff322-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="ff322-210">*API.idpselections*</span><span class="sxs-lookup"><span data-stu-id="ff322-210">*api.idpselections*</span></span> | <span data-ttu-id="ff322-211">**Strona wyboru dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="ff322-211">**Identity provider selection page**.</span></span> <span data-ttu-id="ff322-212">Ta strona zawiera listę dostawców tożsamości, które użytkownik może wybrać podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="ff322-212">This page contains a list of identity providers that the user can choose from during sign-in.</span></span> <span data-ttu-id="ff322-213">Te opcje są enterprise dostawców tożsamości, dostawców tożsamości społecznościowych, takich jak Facebook i Google + lub kont lokalnych.</span><span class="sxs-lookup"><span data-stu-id="ff322-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="ff322-214">*API.idpselections.Signup*</span><span class="sxs-lookup"><span data-stu-id="ff322-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="ff322-215">**Wybór dostawcy tożsamości dla rejestracji**.</span><span class="sxs-lookup"><span data-stu-id="ff322-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="ff322-216">Ta strona zawiera listę dostawców tożsamości, które użytkownik może wybrać podczas tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="ff322-216">This page contains a list of identity providers that the user can choose from during sign-up.</span></span> <span data-ttu-id="ff322-217">Te opcje są enterprise dostawców tożsamości, dostawców tożsamości społecznościowych, takich jak Facebook i Google + lub kont lokalnych.</span><span class="sxs-lookup"><span data-stu-id="ff322-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="ff322-218">*API.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="ff322-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="ff322-219">**Nie pamiętasz hasła strony**.</span><span class="sxs-lookup"><span data-stu-id="ff322-219">**Forgot password page**.</span></span> <span data-ttu-id="ff322-220">Ta strona zawiera formularz, który użytkownik należy wykonać, aby zainicjować resetowania hasła.</span><span class="sxs-lookup"><span data-stu-id="ff322-220">This page contains a form that the user must complete to initiate a password reset.</span></span>  |
| <span data-ttu-id="ff322-221">*API.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="ff322-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="ff322-222">**Strona logowania konta lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="ff322-222">**Local account sign-in page**.</span></span> <span data-ttu-id="ff322-223">Ta strona zawiera formularz logowania dla logowania przy użyciu konta lokalnego, która jest oparta na adres e-mail lub nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ff322-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="ff322-224">Formularz może zawierać pola do wprowadzania tekstu, a w polu wprowadzania hasła.</span><span class="sxs-lookup"><span data-stu-id="ff322-224">The form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="ff322-225">*API.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="ff322-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="ff322-226">**Stronę tworzenia konta lokalnego konta**.</span><span class="sxs-lookup"><span data-stu-id="ff322-226">**Local account sign-up page**.</span></span> <span data-ttu-id="ff322-227">Ta strona zawiera formularz zapisów do skorzystania z konta lokalnego, która jest oparta na adres e-mail lub nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ff322-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="ff322-228">Formularz może zawierać różne kontrolki wejściowe, takich jak pola do wprowadzania tekstu, pole wprowadzania hasła przycisk radiowy, jednokrotnym zaznaczeniem pola listy rozwijanej i pól wyboru wielokrotnego wyboru.</span><span class="sxs-lookup"><span data-stu-id="ff322-228">The form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="ff322-229">*API.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="ff322-229">*api.phonefactor*</span></span> | <span data-ttu-id="ff322-230">**Strona uwierzytelniania wieloskładnikowego**.</span><span class="sxs-lookup"><span data-stu-id="ff322-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="ff322-231">Na tej stronie użytkownicy mogą sprawdzić swoje numery telefonów (przy użyciu tekstowych lub głosowych) podczas tworzenia konta lub logowania.</span><span class="sxs-lookup"><span data-stu-id="ff322-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="ff322-232">*API.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="ff322-232">*api.selfasserted*</span></span> | <span data-ttu-id="ff322-233">**Strony rejestracji społecznościowych konta**.</span><span class="sxs-lookup"><span data-stu-id="ff322-233">**Social account sign-up page**.</span></span> <span data-ttu-id="ff322-234">Ta strona zawiera wypełnieniu formularza, który użytkownicy muszą wykonać podczas logowania przy użyciu istniejącego konta od dostawcy tożsamości społecznościowych, takich jak Facebook lub Google +.</span><span class="sxs-lookup"><span data-stu-id="ff322-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="ff322-235">Ta strona jest podobny do poprzedniego konta społecznościowych stronę tworzenia konta, z wyjątkiem pól wprowadzania hasła.</span><span class="sxs-lookup"><span data-stu-id="ff322-235">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="ff322-236">*API.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="ff322-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="ff322-237">**Strona aktualizacji profilu**.</span><span class="sxs-lookup"><span data-stu-id="ff322-237">**Profile update page**.</span></span> <span data-ttu-id="ff322-238">Ta strona zawiera formularz, który użytkownicy mogą używać do aktualizacji profilu.</span><span class="sxs-lookup"><span data-stu-id="ff322-238">This page contains a form that users can use to update their profile.</span></span> <span data-ttu-id="ff322-239">Ta strona jest podobna do strony rejestracji społecznościowych konto, z wyjątkiem pól wprowadzania hasła.</span><span class="sxs-lookup"><span data-stu-id="ff322-239">This page is similar to the social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="ff322-240">*API.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="ff322-240">*api.signuporsignin*</span></span> | <span data-ttu-id="ff322-241">**Ujednolicone stronę tworzenia konta lub logowania**.</span><span class="sxs-lookup"><span data-stu-id="ff322-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="ff322-242">Ta strona obsługuje zarówno rejestracji i logowania użytkowników, którzy można używać w organizacji dostawcy tożsamości, dostawców tożsamości społecznościowych, takich jak Facebook lub Google + lub kont lokalnych.</span><span class="sxs-lookup"><span data-stu-id="ff322-242">This page handles both the sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="ff322-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff322-243">Next steps</span></span>

<span data-ttu-id="ff322-244">Aby uzyskać dodatkowe informacje na temat elementy interfejsu użytkownika, które można dostosowywać, zobacz [Podręcznik do dostosowania interfejsu użytkownika dla zasad wbudowany](active-directory-b2c-reference-ui-customization.md).</span><span class="sxs-lookup"><span data-stu-id="ff322-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
