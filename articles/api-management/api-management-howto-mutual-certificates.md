---
title: "Bezpieczne usługi zaplecza przy użyciu klienta uwierzytelniania certyfikatów - Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zabezpieczyć usług zaplecza w usłudze Azure API Management przy użyciu wstępnego uwierzytelniania certyfikatu klienta."
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
ms.openlocfilehash: 2ebe71c96fd9076a48f689041634dbd23d3d8414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="4f3be-103">Jak zabezpieczyć za pomocą klienta usług zaplecza certyfikatów uwierzytelniania w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="4f3be-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="4f3be-104">Zarządzanie interfejsami API umożliwia bezpieczny dostęp do usługi zaplecza interfejsu API przy użyciu certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="4f3be-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="4f3be-105">Ten przewodnik zawiera sposobu zarządzania certyfikatami w portalu wydawcy interfejsu API i Konfigurowanie interfejsu API do używania certyfikatu dostęp do jej usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4f3be-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="4f3be-106">Aby uzyskać informacje o zarządzaniu certyfikatami przy użyciu interfejsu API REST zarządzania interfejsu API, zobacz [jednostki certyfikat interfejsu API REST zarządzania interfejsu API platformy Azure][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="4f3be-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="4f3be-107"><a name="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4f3be-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="4f3be-108">W tym przewodniku przedstawiono sposób skonfigurować wystąpienie usługi Zarządzanie interfejsami API do używania uwierzytelniania certyfikatów klienta do uzyskania dostępu do usługi zaplecza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4f3be-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="4f3be-109">Przed wykonaniem kroków w tym temacie, powinien mieć skonfigurowany na potrzeby uwierzytelniania certyfikatu klienta usługi zaplecza ([do konfigurowania certyfikatów uwierzytelniania w witrynach sieci Web Azure odwoływać się do tego artykułu] [ to configure certificate authentication in Azure WebSites refer to this article]), i mieć dostęp do certyfikat i hasło dla certyfikatu na potrzeby przekazywania w portalu zarządzania interfejsu API wydawcy.</span><span class="sxs-lookup"><span data-stu-id="4f3be-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="4f3be-110"><a name="step1"></a>Przekazywanie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="4f3be-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="4f3be-111">Na początku kliknij opcję **Portal wydawcy** w klasycznej witrynie Azure Portal dla usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="4f3be-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="4f3be-112">Spowoduje to przejście do portalu wydawcy usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="4f3be-112">This takes you to the API Management publisher portal.</span></span>

![Portal wydawcy interfejsu API][api-management-management-console]

> <span data-ttu-id="4f3be-114">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="4f3be-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="4f3be-115">Kliknij przycisk **zabezpieczeń** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie kliknij przycisk **certyfikaty klienta**.</span><span class="sxs-lookup"><span data-stu-id="4f3be-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![Certyfikaty klienta][api-management-security-client-certificates]

<span data-ttu-id="4f3be-117">Aby przekazać nowy certyfikat, kliknij przycisk **przekazywania certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="4f3be-117">To upload a new certificate, click **Upload certificate**.</span></span>

![Przekazywanie certyfikatu][api-management-upload-certificate]

<span data-ttu-id="4f3be-119">Przejdź do swojego certyfikatu, a następnie wprowadź hasło dla certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="4f3be-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="4f3be-120">Certyfikat musi być w **PFX** format.</span><span class="sxs-lookup"><span data-stu-id="4f3be-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="4f3be-121">Certyfikaty z podpisem własnym są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="4f3be-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Przekazywanie certyfikatu][api-management-upload-certificate-form]

<span data-ttu-id="4f3be-123">Kliknij przycisk **przekazać** można przekazać certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="4f3be-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="4f3be-124">Hasło certyfikatu jest weryfikowana w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="4f3be-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="4f3be-125">Jeśli jest nieprawidłowe, zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="4f3be-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Przekazany certyfikat][api-management-certificate-uploaded]

<span data-ttu-id="4f3be-127">Po przesłaniu certyfikatu, pojawi się na **certyfikaty klienta** kartę.</span><span class="sxs-lookup"><span data-stu-id="4f3be-127">Once the certificate is uploaded, it appears on the **Client certificates** tab.</span></span> <span data-ttu-id="4f3be-128">Jeśli istnieje wiele certyfikatów, należy Uwaga podmiot lub cztery ostatnie znaki odcisk palca, które są używane, aby wybrać certyfikat, podczas konfigurowania interfejsu API, aby korzystać z certyfikatów, co opisano w następujących [skonfigurować interfejs API do użycia certyfikat klienta na potrzeby uwierzytelniania bramy] [ Configure an API to use a client certificate for gateway authentication] sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f3be-128">If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="4f3be-129">Aby wyłączyć weryfikacji łańcucha certyfikatu przy użyciu, na przykład certyfikatu z podpisem własnym, wykonaj czynności opisane w tym artykule [elementu](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="4f3be-129">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="4f3be-130"><a name="step1a"></a>Usuwanie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="4f3be-130"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="4f3be-131">Aby usunąć certyfikat, kliknij przycisk **usunąć** obok żądanego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="4f3be-131">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![Usuń certyfikat][api-management-certificate-delete]

<span data-ttu-id="4f3be-133">Kliknij przycisk **tak, usuń go** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="4f3be-133">Click **Yes, delete it** to confirm.</span></span>

![Potwierdzenie usunięcia][api-management-confirm-delete]

<span data-ttu-id="4f3be-135">Jeśli certyfikat jest używany przez interfejs API, a następnie zostanie wyświetlony ekran ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="4f3be-135">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="4f3be-136">Aby usunąć certyfikat należy najpierw usunąć certyfikat z żadnych interfejsów API, które są skonfigurowane do używania go.</span><span class="sxs-lookup"><span data-stu-id="4f3be-136">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![Potwierdzenie usunięcia][api-management-confirm-delete-policy]

## <span data-ttu-id="4f3be-138"><a name="step2"></a>Skonfigurować interfejs API do używania certyfikatu klienta uwierzytelniania bramy</span><span class="sxs-lookup"><span data-stu-id="4f3be-138"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="4f3be-139">Kliknij przycisk **interfejsów API** z **zarządzanie interfejsami API** menu po lewej stronie kliknij nazwę żądanego interfejsu API, a następnie kliknij przycisk **zabezpieczeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="4f3be-139">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![Zabezpieczeń interfejsu API][api-management-api-security]

<span data-ttu-id="4f3be-141">Wybierz **certyfikaty klienta** z **przy użyciu poświadczeń** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="4f3be-141">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![Certyfikaty klienta][api-management-mutual-certificates]

<span data-ttu-id="4f3be-143">Wybierz żądany certyfikat z **certyfikatu klienta** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="4f3be-143">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="4f3be-144">Jeśli dostępnych jest wiele certyfikatów można przyjrzeć się podmiot lub cztery ostatnie znaki odcisk palca, zgodnie z opisem w poprzedniej sekcji, aby określić odpowiedni certyfikat.</span><span class="sxs-lookup"><span data-stu-id="4f3be-144">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![Wybierz certyfikat][api-management-select-certificate]

<span data-ttu-id="4f3be-146">Kliknij przycisk **zapisać** można zapisać zmiany konfiguracji do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4f3be-146">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="4f3be-147">Ta zmiana zaczyna się od razu i wywołania operacji tego interfejsu API będzie używany certyfikat do uwierzytelniania na serwerze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4f3be-147">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![Zapisz zmiany interfejsu API][api-management-save-api]

> <span data-ttu-id="4f3be-149">Jeśli nie określono certyfikatu bramy uwierzytelniania usługi zaplecza interfejsu API, staje się częścią zasad dla tego interfejsu API i mogą być wyświetlane w edytorze zasad.</span><span class="sxs-lookup"><span data-stu-id="4f3be-149">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![Zasady certyfikatów][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="4f3be-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f3be-151">Next steps</span></span>
<span data-ttu-id="4f3be-152">Aby uzyskać więcej informacji na inne metody zabezpieczania usługi wewnętrznej bazy danych, takich jak HTTP uwierzytelniania podstawowego lub udostępnionego tajne zobacz poniższe wideo.</span><span class="sxs-lookup"><span data-stu-id="4f3be-152">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

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



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps



