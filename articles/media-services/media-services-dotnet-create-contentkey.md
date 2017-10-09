---
title: "aaaCreate ContentKeys z platformą .NET"
description: "Dowiedz się, jak toocreate kluczy zawartości, które udostępniają bezpieczne dostępu tooAssets."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a>Utwórz ContentKeys z platformą .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

Usługi Media Services umożliwia toocreate i dostarczanie zaszyfrowanych zasoby. A **ContentKey** zapewnia bezpieczny dostęp tooyour **zasobów**s. 

Podczas tworzenia nowego elementu zawartości (na przykład przed [przekazać pliki](media-services-dotnet-upload-files.md)), można określić następujące opcje szyfrowania hello: **StorageEncrypted**, **CommonEncryptionProtected**, lub **EnvelopeEncryptionProtected**. 

Podczas dostarczania zasoby tooyour klientów można [skonfigurować zasoby toobe dynamicznie szyfrowany](media-services-dotnet-configure-asset-delivery-policy.md) z jednym hello następujące dwie metody szyfrowania: **DynamicEnvelopeEncryption** lub  **DynamicCommonEncryption**.

Zasoby zaszyfrowanych ma toobe skojarzone z **ContentKey**s. W tym artykule opisano sposób toocreate klucz zawartości.

> [!NOTE]
> Podczas tworzenia nowego **StorageEncrypted** zasobów przy użyciu hello SDK .NET usługi Media Services, hello **ContentKey** jest automatycznie tworzony i połączone z zasobów hello.
> 
> 

## <a name="contentkeytype"></a>ContentKeyType
Jedna z wartości hello, że należy ustawić podczas tworzenia zawartości klucz jest hello typu klucza zawartości. Wybierz jedną z hello następujące wartości. 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }

## <a id="envelope_contentkey"></a>Tworzenie typu koperty ContentKey
Witaj poniższy fragment kodu tworzy klucz zawartości typu szyfrowania koperty hello. Następnie kojarzy klucz hello z określonym zasobie hello.

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

Wywołania

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a>Tworzenie wspólnego typu ContentKey
Witaj poniższy fragment kodu tworzy klucz zawartości hello wspólnego typu szyfrowania. Następnie kojarzy klucz hello z określonym zasobie hello.

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate hello key with hello asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
Wywołania

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

