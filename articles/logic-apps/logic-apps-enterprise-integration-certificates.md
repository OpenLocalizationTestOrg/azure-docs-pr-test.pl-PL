---
title: "z pakiet integracyjny dla przedsiębiorstw przy użyciu certyfikatów aaaUsing | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse certyfikaty z hello pakiet integracyjny dla przedsiębiorstw | Aplikacje logiki platformy Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="c411d-103">Informacje na temat certyfikatów i pakietu integracyjnego dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="c411d-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="c411d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c411d-104">Overview</span></span>
<span data-ttu-id="c411d-105">Integracja przedsiębiorstwa używa komunikacji B2B toosecure certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="c411d-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="c411d-106">Można użyć dwóch typów certyfikatów, w aplikacjach integracji przedsiębiorstwa:</span><span class="sxs-lookup"><span data-stu-id="c411d-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="c411d-107">Certyfikaty publiczne, które muszą być zakupione od urzędu certyfikacji (CA).</span><span class="sxs-lookup"><span data-stu-id="c411d-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="c411d-108">Certyfikaty prywatne, które można wystawić samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="c411d-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="c411d-109">Te certyfikaty są czasami określonego tooas certyfikaty z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="c411d-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="c411d-110">Co to są certyfikaty?</span><span class="sxs-lookup"><span data-stu-id="c411d-110">What are certificates?</span></span>
<span data-ttu-id="c411d-111">Certyfikaty są cyfrowe dokumentów, który zweryfikować tożsamość hello hello uczestników łączności elektronicznej i który również bezpieczna komunikacja elektronicznej.</span><span class="sxs-lookup"><span data-stu-id="c411d-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="c411d-112">Dlaczego warto używać certyfikatów?</span><span class="sxs-lookup"><span data-stu-id="c411d-112">Why use certificates?</span></span>
<span data-ttu-id="c411d-113">Czasami komunikacji B2B musi poufne.</span><span class="sxs-lookup"><span data-stu-id="c411d-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="c411d-114">Integracji przedsiębiorstwa używa certyfikatów toosecure otrzymywania tych wiadomości na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="c411d-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="c411d-115">Szyfrując hello zawartość wiadomości</span><span class="sxs-lookup"><span data-stu-id="c411d-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="c411d-116">Przez cyfrowego podpisywania wiadomości</span><span class="sxs-lookup"><span data-stu-id="c411d-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="c411d-117">Przekaż certyfikat publiczny</span><span class="sxs-lookup"><span data-stu-id="c411d-117">Upload a public certificate</span></span>

<span data-ttu-id="c411d-118">toouse *certyfikatu publicznego* w aplikacjach logiki z możliwościami B2B, najpierw tooupload hello certyfikatu do konta integracji.</span><span class="sxs-lookup"><span data-stu-id="c411d-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="c411d-119">Po przekazaniu certyfikat jest dostępny toohelp zabezpieczenia wiadomości B2B podczas definiowania ich właściwości w hello [umowy](logic-apps-enterprise-integration-agreements.md) utworzony.</span><span class="sxs-lookup"><span data-stu-id="c411d-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="c411d-120">Poniżej przedstawiono szczegółowe informacje na temat przekazywania certyfikaty publiczne na koncie integracji, po zalogowaniu w portalu Azure toohello hello:</span><span class="sxs-lookup"><span data-stu-id="c411d-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="c411d-121">Wybierz **więcej usług** , a następnie wprowadź **integracji** w polu wyszukiwania hello filtru.</span><span class="sxs-lookup"><span data-stu-id="c411d-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="c411d-122">Wybierz **konta integracji** z hello listy wyników</span><span class="sxs-lookup"><span data-stu-id="c411d-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="c411d-123">![Wybierz opcję Przeglądaj](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="c411d-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="c411d-124">Wybierz toowhich konta integracji hello ma tooadd hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c411d-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Wybierz toowhich konta integracji hello ma tooadd hello certyfikatu](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="c411d-126">Wybierz hello **certyfikaty** kafelka.</span><span class="sxs-lookup"><span data-stu-id="c411d-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="c411d-127">![Certyfikaty hello wybierz Kafelek](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="c411d-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="c411d-128">W hello **certyfikaty** bloku, który zostanie otwarty, wybierz hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c411d-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="c411d-129">![Kliknij przycisk Dodaj hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="c411d-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="c411d-130">Wprowadź **nazwa** dla certyfikatu, a następnie wybierz opcję hello typ certyfikatu jako **publicznego** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="c411d-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="c411d-131">Ikona folderu wybierz powitania po prawej stronie powitania hello **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c411d-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="c411d-132">Po otwarciu hello selektor plików, Znajdź i wybierz plik certyfikatu hello, które mają tooupload tooyour integracji konta.</span><span class="sxs-lookup"><span data-stu-id="c411d-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="c411d-133">Wybierz certyfikat hello, a następnie wybierz **OK** w hello selektor plików.</span><span class="sxs-lookup"><span data-stu-id="c411d-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="c411d-134">Weryfikuje i przekazuje hello certyfikatu tooyour integracji konta.</span><span class="sxs-lookup"><span data-stu-id="c411d-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="c411d-135">Na koniec kopii na powitania **Dodaj certyfikat** bloku, wybierz hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c411d-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="c411d-136">![Wybierz przycisk OK hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="c411d-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="c411d-137">Wybierz hello **certyfikaty** kafelka.</span><span class="sxs-lookup"><span data-stu-id="c411d-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="c411d-138">Powinien pojawić się hello nowo dodany certyfikat.</span><span class="sxs-lookup"><span data-stu-id="c411d-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="c411d-139">![Zobacz hello nowego certyfikatu](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="c411d-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="c411d-140">Przekaż certyfikat prywatny</span><span class="sxs-lookup"><span data-stu-id="c411d-140">Upload a private certificate</span></span>

<span data-ttu-id="c411d-141">toouse *certyfikatu prywatnego* w aplikacjach logiki z możliwościami B2B, możesz przekazać konto integracji tooyour certyfikatu prywatnego przez pobieranie hello następujące kroki</span><span class="sxs-lookup"><span data-stu-id="c411d-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="c411d-142">[Przekaż sieci prywatnej tooKey klucza magazynu](../key-vault/key-vault-get-started.md "więcej informacji na temat usługi Key Vault") i podaj **nazwa klucza**</span><span class="sxs-lookup"><span data-stu-id="c411d-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="c411d-143">Musisz autoryzować Logic Apps tooperform operacje magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="c411d-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="c411d-144">Jednostki usługi Logic Apps toohello dostępu można przyznać za pomocą następującego polecenia programu PowerShell hello:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="c411d-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="c411d-145">Po hello w poprzednim kroku, należy dodać konto toointegration certyfikatu prywatnego.</span><span class="sxs-lookup"><span data-stu-id="c411d-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="c411d-146">Poniżej są hello szczegółowe informacje na temat przekazywania prywatnej certyfikaty do konta integracji, po zalogowaniu toohello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="c411d-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="c411d-147">Wybierz hello integracji konta toowhich tooadd hello certyfikatu a wybrać hello **certyfikaty** kafelka.</span><span class="sxs-lookup"><span data-stu-id="c411d-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="c411d-148">![Certyfikaty hello wybierz Kafelek](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="c411d-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="c411d-149">W hello **certyfikaty** bloku, który zostanie otwarty, wybierz hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c411d-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="c411d-150">![Kliknij przycisk Dodaj hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="c411d-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="c411d-151">Wprowadź **nazwa** dla certyfikatu, a typ certyfikatu wybierz hello jako **prywatnej** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="c411d-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="c411d-152">Wybierz ikonę folder hello na powitania po prawej stronie powitania **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c411d-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="c411d-153">Po otwarciu selektor plików hello znaleźć hello odpowiedniego certyfikatu publicznego, które mają tooupload tooyour integracji konta.</span><span class="sxs-lookup"><span data-stu-id="c411d-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="c411d-154">Podczas dodawania certyfikatu prywatnego jest ważne, tooadd odpowiadającego publicznego certyfikatu tooshow w [umowy AS2](logic-apps-enterprise-integration-as2.md) odbierania i wysyłania ustawień podpisywania i szyfrowania wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="c411d-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="c411d-155">Wybierz hello **grupy zasobów**, **Key Vault**, **nazwa klucza** i wybierz hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c411d-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="c411d-156">![Dodawanie certyfikatu](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="c411d-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="c411d-157">Wybierz hello **certyfikaty** kafelka.</span><span class="sxs-lookup"><span data-stu-id="c411d-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="c411d-158">Powinien pojawić się hello nowo dodany certyfikat.</span><span class="sxs-lookup"><span data-stu-id="c411d-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="c411d-159">![Zobacz hello nowego certyfikatu](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="c411d-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="c411d-160">Tworzenie umowy z B2B</span><span class="sxs-lookup"><span data-stu-id="c411d-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="c411d-161">Dowiedz się więcej na temat usługi Key Vault</span><span class="sxs-lookup"><span data-stu-id="c411d-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "więcej informacji na temat usługi Key Vault")  

