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
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="a4061-103">Utwórz ContentKeys z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="a4061-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4061-104">REST</span><span class="sxs-lookup"><span data-stu-id="a4061-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="a4061-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a4061-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="a4061-106">Usługi Media Services umożliwia toocreate i dostarczanie zaszyfrowanych zasoby.</span><span class="sxs-lookup"><span data-stu-id="a4061-106">Media Services enables you toocreate and deliver encrypted assets.</span></span> <span data-ttu-id="a4061-107">A **ContentKey** zapewnia bezpieczny dostęp tooyour **zasobów**s.</span><span class="sxs-lookup"><span data-stu-id="a4061-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="a4061-108">Podczas tworzenia nowego elementu zawartości (na przykład przed [przekazać pliki](media-services-dotnet-upload-files.md)), można określić następujące opcje szyfrowania hello: **StorageEncrypted**, **CommonEncryptionProtected**, lub **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="a4061-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="a4061-109">Podczas dostarczania zasoby tooyour klientów można [skonfigurować zasoby toobe dynamicznie szyfrowany](media-services-dotnet-configure-asset-delivery-policy.md) z jednym hello następujące dwie metody szyfrowania: **DynamicEnvelopeEncryption** lub  **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="a4061-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="a4061-110">Zasoby zaszyfrowanych ma toobe skojarzone z **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="a4061-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="a4061-111">W tym artykule opisano sposób toocreate klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="a4061-111">This article describes how toocreate a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="a4061-112">Podczas tworzenia nowego **StorageEncrypted** zasobów przy użyciu hello SDK .NET usługi Media Services, hello **ContentKey** jest automatycznie tworzony i połączone z zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="a4061-112">When creating a new **StorageEncrypted** asset using hello Media Services .NET SDK , hello **ContentKey** is automatically created and linked with hello asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="a4061-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="a4061-113">ContentKeyType</span></span>
<span data-ttu-id="a4061-114">Jedna z wartości hello, że należy ustawić podczas tworzenia zawartości klucz jest hello typu klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="a4061-114">One of hello values that you must set when create a content key is hello content key type.</span></span> <span data-ttu-id="a4061-115">Wybierz jedną z hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="a4061-115">Choose from one of hello following values.</span></span> 

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

## <span data-ttu-id="a4061-116"><a id="envelope_contentkey"></a>Tworzenie typu koperty ContentKey</span><span class="sxs-lookup"><span data-stu-id="a4061-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="a4061-117">Witaj poniższy fragment kodu tworzy klucz zawartości typu szyfrowania koperty hello.</span><span class="sxs-lookup"><span data-stu-id="a4061-117">hello following code snippet creates a content key of hello envelope encryption type.</span></span> <span data-ttu-id="a4061-118">Następnie kojarzy klucz hello z określonym zasobie hello.</span><span class="sxs-lookup"><span data-stu-id="a4061-118">It then associates hello key with hello specified asset.</span></span>

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

<span data-ttu-id="a4061-119">Wywołania</span><span class="sxs-lookup"><span data-stu-id="a4061-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="a4061-120"><a id="common_contentkey"></a>Tworzenie wspólnego typu ContentKey</span><span class="sxs-lookup"><span data-stu-id="a4061-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="a4061-121">Witaj poniższy fragment kodu tworzy klucz zawartości hello wspólnego typu szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="a4061-121">hello following code snippet creates a content key of hello common encryption type.</span></span> <span data-ttu-id="a4061-122">Następnie kojarzy klucz hello z określonym zasobie hello.</span><span class="sxs-lookup"><span data-stu-id="a4061-122">It then associates hello key with hello specified asset.</span></span>

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
<span data-ttu-id="a4061-123">Wywołania</span><span class="sxs-lookup"><span data-stu-id="a4061-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="a4061-124">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="a4061-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a4061-125">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="a4061-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

