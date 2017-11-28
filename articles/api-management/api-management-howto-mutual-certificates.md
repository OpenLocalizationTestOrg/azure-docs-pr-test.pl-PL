---
title: "aaaSecure usług zaplecza przy użyciu wstępnego uwierzytelniania certyfikatu klienta - Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak za pomocą klienta usług zaplecza toosecure certyfikatów uwierzytelniania w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="56d8e-103">Jak za pomocą klienta usług zaplecza toosecure certyfikatów uwierzytelniania w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="56d8e-103">How toosecure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="56d8e-104">Zarządzanie interfejsami API udostępnia hello możliwości toosecure dostępu toohello usługi zaplecza interfejsu API przy użyciu certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="56d8e-104">API Management provides hello capability toosecure access toohello back-end service of an API using client certificates.</span></span> <span data-ttu-id="56d8e-105">Ten przewodnik przedstawia, jak toomanage certyfikaty w portalu wydawcy hello interfejsu API i jak toouse tooconfigure API tooaccess certyfikatu jej usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="56d8e-105">This guide shows how toomanage certificates in hello API publisher portal, and how tooconfigure an API toouse a certificate tooaccess its back-end service.</span></span>

<span data-ttu-id="56d8e-106">Aby uzyskać informacje o zarządzaniu certyfikatami przy użyciu interfejsu API REST zarządzania interfejsu API hello, zobacz [jednostki certyfikat interfejsu API REST zarządzania interfejsu API platformy Azure][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="56d8e-106">For information about managing certificates using hello API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="56d8e-107"><a name="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="56d8e-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="56d8e-108">Ten przewodnik przedstawia, jak tooconfigure Twojego zarządzanie interfejsami API usługi wystąpienia toouse klienta certyfikatu uwierzytelniania tooaccess hello usługi zaplecza do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="56d8e-108">This guide shows you how tooconfigure your API Management service instance toouse client certificate authentication tooaccess hello back-end service for an API.</span></span> <span data-ttu-id="56d8e-109">Przed hello następujące kroki w tym temacie, powinien mieć skonfigurowany na potrzeby uwierzytelniania certyfikatu klienta usługi zaplecza ([tooconfigure certyfikatów uwierzytelniania w witrynach sieci Web platformy Azure można znaleźć w artykule toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), i mieć toohello certyfikat i hello hasło dostępu do certyfikatu hello pobierania w portalu wydawcy zarządzanie interfejsami API hello.</span><span class="sxs-lookup"><span data-stu-id="56d8e-109">Before following hello steps in this topic, you should have your back-end service configured for client certificate authentication ([tooconfigure certificate authentication in Azure WebSites refer toothis article][tooconfigure certificate authentication in Azure WebSites refer toothis article]), and have access toohello certificate and hello password for hello certificate for uploading in hello API Management publisher portal.</span></span>

## <span data-ttu-id="56d8e-110"><a name="step1"></a>Przekazywanie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="56d8e-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="56d8e-111">tooget pracę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="56d8e-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="56d8e-112">Trwa toohello zarządzanie interfejsami API wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="56d8e-112">This takes you toohello API Management publisher portal.</span></span>

![Portal wydawcy interfejsu API][api-management-management-console]

> <span data-ttu-id="56d8e-114">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="56d8e-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="56d8e-115">Kliknij przycisk **zabezpieczeń** z hello **zarządzanie interfejsami API** menu po lewej hello i kliknij przycisk **certyfikaty klienta**.</span><span class="sxs-lookup"><span data-stu-id="56d8e-115">Click **Security** from hello **API Management** menu on hello left, and click **Client certificates**.</span></span>

![Certyfikaty klienta][api-management-security-client-certificates]

<span data-ttu-id="56d8e-117">tooupload nowego świadectwa, kliknij przycisk **przekazywania certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="56d8e-117">tooupload a new certificate, click **Upload certificate**.</span></span>

![Przekazywanie certyfikatu][api-management-upload-certificate]

<span data-ttu-id="56d8e-119">Przeglądaj tooyour certyfikatu, a następnie wprowadź hasło hello hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="56d8e-119">Browse tooyour certificate, and then enter hello password for hello certificate.</span></span>

> <span data-ttu-id="56d8e-120">Witaj, certyfikat musi być w **PFX** format.</span><span class="sxs-lookup"><span data-stu-id="56d8e-120">hello certificate must be in **.pfx** format.</span></span> <span data-ttu-id="56d8e-121">Certyfikaty z podpisem własnym są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="56d8e-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Przekazywanie certyfikatu][api-management-upload-certificate-form]

<span data-ttu-id="56d8e-123">Kliknij przycisk **przekazać** tooupload hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="56d8e-123">Click **Upload** tooupload hello certificate.</span></span>

> <span data-ttu-id="56d8e-124">Hasło certyfikatu Hello jest weryfikowana w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="56d8e-124">hello certificate password is validated at this time.</span></span> <span data-ttu-id="56d8e-125">Jeśli jest nieprawidłowe, zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="56d8e-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Przekazany certyfikat][api-management-certificate-uploaded]

<span data-ttu-id="56d8e-127">Po przekazaniu hello certyfikatu znajdującego się na powitania **certyfikaty klienta** kartę. Jeśli masz wiele certyfikatów, zanotuj hello podmiotu lub hello cztery ostatnie znaki hello odcisku palca, które są używane tooselect hello certyfikatu podczas konfigurowania toouse interfejsu API certyfikaty, jak to opisano w następujących hello [Konfiguruj Interfejs API toouse certyfikat klienta na potrzeby uwierzytelniania bramy] [ Configure an API toouse a client certificate for gateway authentication] sekcji.</span><span class="sxs-lookup"><span data-stu-id="56d8e-127">Once hello certificate is uploaded, it appears on hello **Client certificates** tab. If you have multiple certificates, make a note of hello subject, or hello last four characters of hello thumbprint, which are used tooselect hello certificate when configuring an API toouse certificates, as covered in hello following [Configure an API toouse a client certificate for gateway authentication][Configure an API toouse a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="56d8e-128">tooturn poza weryfikacji łańcucha certyfikatu w przypadku korzystania na przykład certyfikatu z podpisem własnym, wykonaj kroki hello opisane w tym artykule [elementu](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="56d8e-128">tooturn off certificate chain validation when using, for example, a self-signed certificate, follow hello steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="56d8e-129"><a name="step1a"></a>Usuwanie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="56d8e-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="56d8e-130">toodelete certyfikat, kliknij przycisk **usunąć** obok hello żądanego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="56d8e-130">toodelete a certificate, click **Delete** beside hello desired certificate.</span></span>

![Usuń certyfikat][api-management-certificate-delete]

<span data-ttu-id="56d8e-132">Kliknij przycisk **tak, usuń go** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="56d8e-132">Click **Yes, delete it** tooconfirm.</span></span>

![Potwierdzenie usunięcia][api-management-confirm-delete]

<span data-ttu-id="56d8e-134">Jeśli certyfikat hello jest używany przez interfejs API, wyświetlany jest ekran z ostrzeżeniem.</span><span class="sxs-lookup"><span data-stu-id="56d8e-134">If hello certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="56d8e-135">toodelete hello certyfikatów, należy najpierw usunąć hello certyfikatów wszystkie interfejsy API, które są skonfigurowane toouse go.</span><span class="sxs-lookup"><span data-stu-id="56d8e-135">toodelete hello certificate you must first remove hello certificate from any APIs that are configured toouse it.</span></span>

![Potwierdzenie usunięcia][api-management-confirm-delete-policy]

## <span data-ttu-id="56d8e-137"><a name="step2"></a>Skonfigurować toouse interfejsu API certyfikat klienta na potrzeby uwierzytelniania bramy</span><span class="sxs-lookup"><span data-stu-id="56d8e-137"><a name="step2"> </a>Configure an API toouse a client certificate for gateway authentication</span></span>
<span data-ttu-id="56d8e-138">Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, kliknij nazwę hello hello żądanego interfejsu API, a następnie kliknij przycisk hello **zabezpieczeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="56d8e-138">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, and click hello **Security** tab.</span></span>

![Zabezpieczeń interfejsu API][api-management-api-security]

<span data-ttu-id="56d8e-140">Wybierz **certyfikaty klienta** z hello **przy użyciu poświadczeń** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="56d8e-140">Select **Client certificates** from hello **With credentials** drop-down list.</span></span>

![Certyfikaty klienta][api-management-mutual-certificates]

<span data-ttu-id="56d8e-142">Wybierz hello żądany certyfikat z hello **certyfikatu klienta** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="56d8e-142">Select hello desired certificate from hello **Client certificate** drop-down list.</span></span> <span data-ttu-id="56d8e-143">Jeśli dostępnych jest wiele certyfikatów można przeglądać temat hello i hello cztery ostatnie znaki hello odcisk palca, zgodnie z opisem w hello poprzedniej sekcji toodetermine hello prawidłowego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="56d8e-143">If there are multiple certificates you can look at hello subject or hello last four characters of hello thumbprint as noted in hello previous section toodetermine hello correct certificate.</span></span>

![Wybierz certyfikat][api-management-select-certificate]

<span data-ttu-id="56d8e-145">Kliknij przycisk **zapisać** toosave hello konfiguracji zmiany toohello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="56d8e-145">Click **Save** toosave hello configuration change toohello API.</span></span>

> <span data-ttu-id="56d8e-146">Ta zmiana zaczyna się od razu i tooauthenticate certyfikatu na serwerze zaplecza hello hello wywołania używanego toooperations tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="56d8e-146">This change is effective immediately, and calls toooperations of that API will use hello certificate tooauthenticate on hello back-end server.</span></span>
> 
> 

![Zapisz zmiany interfejsu API][api-management-save-api]

> <span data-ttu-id="56d8e-148">Jeśli nie określono certyfikatu uwierzytelniania bramy hello usługi zaplecza interfejsu API, staje się częścią hello zasad dla tego interfejsu API i można wyświetlić w edytorze zasad hello.</span><span class="sxs-lookup"><span data-stu-id="56d8e-148">When a certificate is specified for gateway authentication for hello back-end service of an API, it becomes part of hello policy for that API, and can be viewed in hello policy editor.</span></span>
> 
> 

![Zasady certyfikatów][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="56d8e-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="56d8e-150">Next steps</span></span>
<span data-ttu-id="56d8e-151">Aby uzyskać więcej informacji na temat innych sposobów toosecure usługi wewnętrznej bazy danych, takich jak HTTP uwierzytelniania podstawowego lub udostępnionego tajne, zobacz powitania po wideo.</span><span class="sxs-lookup"><span data-stu-id="56d8e-151">For more information on other ways toosecure your backend service, such as HTTP basic or shared secret authentication, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



