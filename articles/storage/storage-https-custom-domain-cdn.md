---
title: "obiekty BLOB tooaccess Azure CDN hello aaaUsing z domenami niestandardowymi za pośrednictwem protokołu HTTPS"
description: "Dowiedz się, jak toointegrate hello Azure CDN z tooaccess magazynu obiektów blob, obiekty BLOB z domenami niestandardowymi za pośrednictwem protokołu HTTPS"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: 678e24a7dde5cb2f8feea177bb47c92f61035e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a>Używanie hello Azure CDN tooaccess blob z domenami niestandardowymi za pośrednictwem protokołu HTTPS

Azure sieci dostarczania zawartości (CDN) obsługuje teraz HTTPS dla niestandardowych nazw domen.
Można korzystać z tej funkcji tooaccess magazynu obiektów blob przy użyciu domeny niestandardowej przy użyciu protokołu HTTPS. toodo tak, musisz najpierw tooenable Azure CDN na obiekt blob punktu końcowego, a następnie mapować hello CDN tooa niestandardową nazwę domeny. Po wykonaniu tych kroków, włączanie obsługi protokołu HTTPS dla domeny niestandardowej jest uproszczone, za pomocą pełnego zarządzania certyfikatami, na jednym kliknięciem włączenie i wszystkie nie dodatkowych kosztów toonormal sieci CDN w warstwie cenowej.

Ta możliwość jest ważne, ponieważ umożliwia ona możesz tooprotect hello prywatność i integralność danych aplikacji sieci web poufne przesyłane. Przy użyciu hello ruchu tooserve protokołu SSL za pośrednictwem protokołu HTTPS powodują szyfrowanie danych przesyłanych przez hello internet. HTTPS zapewnia zaufania i uwierzytelniania, a następnie chroni przed atakami aplikacji sieci web.

> [!NOTE]
> Ponadto tooproviding obsługi protokołu SSL dla nazwy domeny niestandardowej, hello Azure CDN może ułatwić skalowanie zawartości wysokiej przepustowości toodeliver aplikacji wokół hello world.
> toolearn więcej, zapoznaj się z [omówienie hello Azure CDN](../cdn/cdn-overview.md).
>
>

## <a name="quick-start"></a>Szybki start

Są to hello kroki wymagane tooenable HTTPS dla punktu końcowego magazynu niestandardowego obiektu blob:

1.  [Integracja z usługą Azure CDN konta magazynu platformy Azure](../cdn/cdn-create-a-storage-account-with-cdn.md).
    Ten artykuł przeprowadzi Cię przez proces tworzenia konta magazynu w hello portalu Azure, jeśli nie zostało to jeszcze zrobione.
2.  [Domen niestandardowych tooa zawartości mapy usługi Azure CDN](../cdn/cdn-map-content-to-custom-domain.md).
3.  [Włącz protokół HTTPS na domenę niestandardową Azure CDN](../cdn/cdn-custom-ssl.md).

## <a name="shared-access-signatures"></a>Sygnatury dostępu współdzielonego

Jeśli punktu końcowego magazynu obiektów blob jest skonfigurowany toodisallow anonimowy dostęp do odczytu, konieczne będzie tooprovide [dostępu sygnatury dostępu Współdzielonego](storage-dotnet-shared-access-signature-part-1.md) tokenu w każdym żądaniu wprowadzeniu tooyour domeny niestandardowej. Domyślnie punkty końcowe magazynu obiektów blob nie zezwalaj na anonimowy dostęp do odczytu. Zobacz [Zarządzanie anonimowy dostęp do odczytu do kontenerów i obiektów blob](storage-manage-access-to-resources.md) Aby uzyskać więcej informacji na temat sygnatur dostępu współdzielonego.

Usługi Azure CDN nie przestrzega tokenu sygnatury dostępu Współdzielonego toohello dodano żadnych ograniczeń. Na przykład wszystkie tokeny sygnatury dostępu Współdzielonego ma czasu wygaśnięcia. Oznacza to, że zawartość nadal będą dostępne z wygasłych SAS, aż do tej zawartości jest przeczyszczone hello CDN krawędzi węzłów. Można kontrolować, jak długo dane są buforowane na powitania CDN przez ustawienie nagłówka odpowiedzi hello pamięci podręcznej. Zobacz [zarządzaniu wygasaniem obiektów blob magazynu Azure w usłudze Azure CDN](../cdn/cdn-manage-expiration-of-blob-content.md) instrukcje.

W przypadku utworzenia wielu skojarzeń zabezpieczeń adresy URL hello tego samego obiektu blob punktu końcowego, zalecamy włączenie buforowanie ciągu zapytania dla Twojej usługi Azure CDN. Jest to tooensure który każdego adresu URL jest traktowany jako unikatowe jednostki. Zobacz [kontrolowanie Azure CDN buforowanie z ciągami zapytań](../cdn/cdn-query-string.md) Aby uzyskać więcej informacji.

## <a name="http-toohttps-redirection"></a>Przekierowywanie HTTP tooHTTPS

Można wybrać tooHTTPS ruch HTTP tooredirect. Wymaga to użycia hello Azure CDN premium oferty from Verizon. Należy zbyt[zachowanie zastąpienie HTTP przy użyciu usługi Azure CDN aparatu reguł](../cdn/cdn-rules-engine.md) z następującą regułą:

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

"Nazwa Cdn — punktu końcowego" odwołuje się nazwa toohello, skonfigurowanego dla punktu końcowego CDN. Tę wartość można wybrać z listy rozwijanej hello. "— Ścieżka do źródła" odnosi się do ścieżki hello w ramach konta magazynu pochodzenia, gdzie znajduje się zawartości statycznej.
Jeśli przechowujesz całej zawartości statycznej w jeden kontener Zamień hello nazwę tego kontenera "— Ścieżka do źródła".

Bardziej zgłębić temat do zasad, zobacz hello [zasady usługi Azure CDN aparat funkcji](../cdn/cdn-rules-engine-reference-features.md).

## <a name="pricing-and-billing"></a>Cennik i rozliczenia

Gdy uzyskujesz dostęp do obiektów blob za pośrednictwem usługi Azure CDN, płacisz [obiektu Blob magazynu ceny](https://azure.microsoft.com/pricing/details/storage/blobs/) dla ruchu między węzłami krawędzi hello a hello pochodzenia (magazynu obiektów Blob) i [ceny CDN](https://azure.microsoft.com/pricing/details/cdn/) z węzłów krawędzi hello uzyskać dostępu do danych.

Na przykład załóżmy, że konto magazynu w zachodnie stany USA, który jest uzyskiwany za pomocą usługi Azure CDN. Jeśli w hello UK spróbuje tooaccess jedną hello obiekty BLOB na tym koncie magazynu za pośrednictwem hello CDN, Azure najpierw sprawdza węzeł brzegowy hello najbliżej hello UK dla tego obiektu blob. Jeśli znaleziono, jego uzyskuje dostęp do tej kopii obiektu blob hello i użyje cennik usługi CDN, ponieważ jest on dostępny na powitania CDN. Jeśli nie zostanie znaleziony, Azure skopiuje węzłem krawędzi toohello obiektu blob hello, co spowoduje transfer danych wychodzących i opłat transakcji jako hello określony w obiektu Blob magazynu ceny i uzyskuje dostęp do pliku hello na węzeł brzegowy hello, co spowoduje rozliczeń CDN.

Podczas przeglądania hello [cennik usługi CDN](https://azure.microsoft.com/pricing/details/cdn/), należy pamiętać, że obsługa protokołu HTTPS dla niestandardowych nazw domen jest dostępna tylko dla usługi Azure CDN z produktów Verizon (Standard i Premium).

## <a name="next-steps"></a>Następne kroki

[Konfigurowanie niestandardowej nazwy domeny dla punktu końcowego magazynu obiektów Blob](storage-custom-domain-name.md)
