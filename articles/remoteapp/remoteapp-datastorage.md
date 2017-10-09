---
title: "poufne dane aaaNever magazyn na niestandardowych obrazów dla usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wytycznych hello do przechowywania danych w niestandardowych obrazów w usłudze Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="61237-103">Nigdy nie przechowują dane poufne na niestandardowych obrazów</span><span class="sxs-lookup"><span data-stu-id="61237-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61237-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="61237-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="61237-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="61237-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="61237-106">Kiedy host aplikacji w usłudze Azure RemoteApp, pierwszym krokiem hello jest toocreate niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="61237-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="61237-107">Korzystamy z tego obrazu niestandardowego wystąpień maszyn wirtualnych toocreate obsługujących aplikacje tooyour użytkowników.</span><span class="sxs-lookup"><span data-stu-id="61237-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="61237-108">niestandardowy obraz powitania powinna zawierać tylko aplikacji i nigdy nie poufnych danych, które mogą zostać utracone, takie jak bazy danych SQL, pliki personelu lub plików danych specjalnych, takich jak pliki firmy QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="61237-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="61237-109">Wszystkie dane poufne powinien znajdować się tooAzure zewnętrznych RemoteApp na serwerze plików z innej maszyny Wirtualnej platformy Azure lub w usługach SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="61237-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="61237-110">Obraz powitania powinien tylko aplikacji hello hosta, która łączy toohello źródła danych i przedstawia hello danych.</span><span class="sxs-lookup"><span data-stu-id="61237-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="61237-111">Przegląd [wymagania dotyczące usługi Azure RemoteApp obrazów](remoteapp-imagereqs.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="61237-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="61237-112">toounderstand, dlaczego nie należy przechowywać poufnych danych, należy toounderstand sposób działania usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="61237-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="61237-113">Podczas tworzenia lub aktualizowania kolekcji tle hello wielu klony lub kopii obrazu hello są tworzone.</span><span class="sxs-lookup"><span data-stu-id="61237-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="61237-114">Wszystkie wystąpienia maszyny Wirtualnej są dokładne repliki hello niestandardowego obrazu; gdy użytkownicy uruchomią aplikacji są połączone tooone tych wystąpień maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61237-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="61237-115">Jednak hello tego samego wystąpienia nie jest gwarantowana i powinien niezależnie od tego, ponieważ są one trwałe.</span><span class="sxs-lookup"><span data-stu-id="61237-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="61237-116">Witaj wystąpień maszyn wirtualnych hostingu aplikacji hello są trwałe i mogą być zniszczony lub usunięty, opartych na przykład podczas aktualizowania kolekcji.</span><span class="sxs-lookup"><span data-stu-id="61237-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="61237-117">Po zainicjowaniu obsługi zbierania hello i użytkownicy uruchamiają łączącego toohello maszyny wirtualne, dane użytkownika są trwałe i chronić, ponieważ są one zapisywane na oddzielnych magazynu w ramach dysku VHD, który nazywamy [dysku profilu użytkownika (UPD)](remoteapp-upd.md), która jest hello profilu użytkownika w c:\users\<userprofile >.</span><span class="sxs-lookup"><span data-stu-id="61237-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="61237-118">Po uruchomieniu aplikacji hello UPD jest instalowana i traktowany tak samo jak lokalny profil użytkownika przez system operacyjny hello.</span><span class="sxs-lookup"><span data-stu-id="61237-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="61237-119">Dowiedz się więcej o jak [usługi Azure RemoteApp zapisuje dane użytkownika i ustawienia](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="61237-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="61237-120">Przykładowe dane, który nie powinien znajdować się w obrazie hello:</span><span class="sxs-lookup"><span data-stu-id="61237-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="61237-121">Udostępnionych danych dla użytkowników tooaccess</span><span class="sxs-lookup"><span data-stu-id="61237-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="61237-122">Baza danych SQL lub bazy danych programu QuickBooks</span><span class="sxs-lookup"><span data-stu-id="61237-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="61237-123">Wszystkie dane w D:\\</span><span class="sxs-lookup"><span data-stu-id="61237-123">Any data in D:\\</span></span>

<span data-ttu-id="61237-124">Przykładowe dane, które mogą znajdować się w toobe profil domyślny hello są kopiowane do UPD co użytkowników:</span><span class="sxs-lookup"><span data-stu-id="61237-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="61237-125">Pliki konfiguracji na użytkownika</span><span class="sxs-lookup"><span data-stu-id="61237-125">Configuration files per user</span></span>
* <span data-ttu-id="61237-126">Skrypty, które użytkownicy czy muszą być zachowane w ich UPD</span><span class="sxs-lookup"><span data-stu-id="61237-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="61237-127">Kwestie kluczowe:</span><span class="sxs-lookup"><span data-stu-id="61237-127">Key points:</span></span>

* <span data-ttu-id="61237-128">Nigdy nie przechowują dane poufne, które można utracić hello obrazu podczas tworzenia niestandardowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="61237-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="61237-129">Dane poufne zawsze powinien znajdować się na oddzielnym serwerze plików, oddziel maszyny Wirtualnej platformy Azure w chmurze hello i wystąpień maszyny Wirtualnej zawsze zewnętrznych toohello hosting aplikacji w usłudze Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="61237-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="61237-130">Dane użytkownika są zapisywane i będzie się powtarzał dysku profilu użytkownika hello (UPD)</span><span class="sxs-lookup"><span data-stu-id="61237-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

