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
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Jak za pomocą klienta usług zaplecza toosecure certyfikatów uwierzytelniania w usłudze Azure API Management
Zarządzanie interfejsami API udostępnia hello możliwości toosecure dostępu toohello usługi zaplecza interfejsu API przy użyciu certyfikatów klienta. Ten przewodnik przedstawia, jak toomanage certyfikaty w portalu wydawcy hello interfejsu API i jak toouse tooconfigure API tooaccess certyfikatu jej usługi zaplecza.

Aby uzyskać informacje o zarządzaniu certyfikatami przy użyciu interfejsu API REST zarządzania interfejsu API hello, zobacz [jednostki certyfikat interfejsu API REST zarządzania interfejsu API platformy Azure][Azure API Management REST API Certificate entity].

## <a name="prerequisites"></a>Wymagania wstępne
Ten przewodnik przedstawia, jak tooconfigure Twojego zarządzanie interfejsami API usługi wystąpienia toouse klienta certyfikatu uwierzytelniania tooaccess hello usługi zaplecza do interfejsu API. Przed hello następujące kroki w tym temacie, powinien mieć skonfigurowany na potrzeby uwierzytelniania certyfikatu klienta usługi zaplecza ([tooconfigure certyfikatów uwierzytelniania w witrynach sieci Web platformy Azure można znaleźć w artykule toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), i mieć toohello certyfikat i hello hasło dostępu do certyfikatu hello pobierania w portalu wydawcy zarządzanie interfejsami API hello.

## <a name="step1"></a>Przekazywanie certyfikatu klienta
tooget pracę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API. Trwa toohello zarządzanie interfejsami API wydawcy portalu.

![Portal wydawcy interfejsu API][api-management-management-console]

> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.
> 
> 

Kliknij przycisk **zabezpieczeń** z hello **zarządzanie interfejsami API** menu po lewej hello i kliknij przycisk **certyfikaty klienta**.

![Certyfikaty klienta][api-management-security-client-certificates]

tooupload nowego świadectwa, kliknij przycisk **przekazywania certyfikatu**.

![Przekazywanie certyfikatu][api-management-upload-certificate]

Przeglądaj tooyour certyfikatu, a następnie wprowadź hasło hello hello certyfikatu.

> Witaj, certyfikat musi być w **PFX** format. Certyfikaty z podpisem własnym są dozwolone.
> 
> 

![Przekazywanie certyfikatu][api-management-upload-certificate-form]

Kliknij przycisk **przekazać** tooupload hello certyfikatu.

> Hasło certyfikatu Hello jest weryfikowana w tej chwili. Jeśli jest nieprawidłowe, zostanie wyświetlony komunikat o błędzie.
> 
> 

![Przekazany certyfikat][api-management-certificate-uploaded]

Po przekazaniu hello certyfikatu znajdującego się na powitania **certyfikaty klienta** kartę. Jeśli masz wiele certyfikatów, zanotuj hello podmiotu lub hello cztery ostatnie znaki hello odcisku palca, które są używane tooselect hello certyfikatu podczas konfigurowania toouse interfejsu API certyfikaty, jak to opisano w następujących hello [Konfiguruj Interfejs API toouse certyfikat klienta na potrzeby uwierzytelniania bramy] [ Configure an API toouse a client certificate for gateway authentication] sekcji.

> tooturn poza weryfikacji łańcucha certyfikatu w przypadku korzystania na przykład certyfikatu z podpisem własnym, wykonaj kroki hello opisane w tym artykule [elementu](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).
> 
> 

## <a name="step1a"></a>Usuwanie certyfikatu klienta
toodelete certyfikat, kliknij przycisk **usunąć** obok hello żądanego certyfikatu.

![Usuń certyfikat][api-management-certificate-delete]

Kliknij przycisk **tak, usuń go** tooconfirm.

![Potwierdzenie usunięcia][api-management-confirm-delete]

Jeśli certyfikat hello jest używany przez interfejs API, wyświetlany jest ekran z ostrzeżeniem. toodelete hello certyfikatów, należy najpierw usunąć hello certyfikatów wszystkie interfejsy API, które są skonfigurowane toouse go.

![Potwierdzenie usunięcia][api-management-confirm-delete-policy]

## <a name="step2"></a>Skonfigurować toouse interfejsu API certyfikat klienta na potrzeby uwierzytelniania bramy
Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, kliknij nazwę hello hello żądanego interfejsu API, a następnie kliknij przycisk hello **zabezpieczeń** kartę.

![Zabezpieczeń interfejsu API][api-management-api-security]

Wybierz **certyfikaty klienta** z hello **przy użyciu poświadczeń** listy rozwijanej.

![Certyfikaty klienta][api-management-mutual-certificates]

Wybierz hello żądany certyfikat z hello **certyfikatu klienta** listy rozwijanej. Jeśli dostępnych jest wiele certyfikatów można przeglądać temat hello i hello cztery ostatnie znaki hello odcisk palca, zgodnie z opisem w hello poprzedniej sekcji toodetermine hello prawidłowego certyfikatu.

![Wybierz certyfikat][api-management-select-certificate]

Kliknij przycisk **zapisać** toosave hello konfiguracji zmiany toohello interfejsu API.

> Ta zmiana zaczyna się od razu i tooauthenticate certyfikatu na serwerze zaplecza hello hello wywołania używanego toooperations tego interfejsu API.
> 
> 

![Zapisz zmiany interfejsu API][api-management-save-api]

> Jeśli nie określono certyfikatu uwierzytelniania bramy hello usługi zaplecza interfejsu API, staje się częścią hello zasad dla tego interfejsu API i można wyświetlić w edytorze zasad hello.
> 
> 

![Zasady certyfikatów][api-management-certificate-policy]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat innych sposobów toosecure usługi wewnętrznej bazy danych, takich jak HTTP uwierzytelniania podstawowego lub udostępnionego tajne, zobacz powitania po wideo.

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



