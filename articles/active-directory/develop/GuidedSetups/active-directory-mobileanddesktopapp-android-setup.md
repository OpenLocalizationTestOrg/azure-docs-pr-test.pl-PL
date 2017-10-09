---
title: "aaaAzure AD w wersji 2 dla systemu Android wprowadzenie — Instalator | Dokumentacja firmy Microsoft"
description: "Jak uzyskać token dostępu i wywołania interfejsu API programu Microsoft Graph lub interfejsów API, które wymagają tokenów dostępu z usługą Azure Active Directory v2 końcowego region systemu Android"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="d4902-103">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="d4902-103">Set up your project</span></span>

> <span data-ttu-id="d4902-104">Preferowane projekt programu Android Studio tego przykładu toodownload zamiast niego?</span><span class="sxs-lookup"><span data-stu-id="d4902-104">Prefer toodownload this sample's Android Studio project instead?</span></span> <span data-ttu-id="d4902-105">[Pobieranie projektu](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) i pominąć toohello [kroku konfiguracji](#create-an-application-express) przykładowy kod hello tooconfigure przed wykonaniem.</span><span class="sxs-lookup"><span data-stu-id="d4902-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="d4902-106">Tworzenie nowego projektu</span><span class="sxs-lookup"><span data-stu-id="d4902-106">Create a new project</span></span> 
1.  <span data-ttu-id="d4902-107">Otwórz program Android Studio, przejdź do:`File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="d4902-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="d4902-108">Nazwa aplikacji, a następnie kliknij przycisk`Next`</span><span class="sxs-lookup"><span data-stu-id="d4902-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="d4902-109">Upewnij się, że tooselect *21 interfejsu API lub nowszej (Android 5.0)* i kliknij przycisk`Next`</span><span class="sxs-lookup"><span data-stu-id="d4902-109">Make sure tooselect *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="d4902-110">Pozostaw `Empty Activity`, kliknij przycisk `Next`, następnie`Finish`</span><span class="sxs-lookup"><span data-stu-id="d4902-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="d4902-111">Dodaj projekt tooyour biblioteki uwierzytelniania firmy Microsoft (MSAL) hello</span><span class="sxs-lookup"><span data-stu-id="d4902-111">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1.  <span data-ttu-id="d4902-112">W programie Android Studio przejdź do:`Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="d4902-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="d4902-113">Kopiuj i Wklej hello następujący kod w obszarze `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="d4902-113">Copy and paste hello following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="d4902-114">O tym pakiecie</span><span class="sxs-lookup"><span data-stu-id="d4902-114">About this package</span></span>

<span data-ttu-id="d4902-115">Pakiet HELLO powyżej instaluje hello biblioteki uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="d4902-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="d4902-116">MSAL obsługuje pobieranie, buforowanie i odświeżanie użytkownika tokenów używanych tooaccess interfejsów API chronione przez punkt końcowy w wersji 2 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d4902-116">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="d4902-117">Tworzenie aplikacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d4902-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="d4902-118">Otwórz: `activity_main.xml` w obszarze`res` > `layout`</span><span class="sxs-lookup"><span data-stu-id="d4902-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="d4902-119">Zmień hello działania układ z `android.support.constraint.ConstraintLayout` lub innych zbyt`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="d4902-119">Change hello activity layout from `android.support.constraint.ConstraintLayout` or other too`LinearLayout`</span></span>
3.  <span data-ttu-id="d4902-120">Dodaj `android:orientation="vertical"` właściwości zbyt`LinearLayout` węzła</span><span class="sxs-lookup"><span data-stu-id="d4902-120">Add `android:orientation="vertical"` property too`LinearLayout` node</span></span>
4.  <span data-ttu-id="d4902-121">Kopiuj i wklej następujący hello kodu do hello `LinearLayout` węzła, zastępując hello bieżącej zawartości:</span><span class="sxs-lookup"><span data-stu-id="d4902-121">Copy and paste hello following code into hello `LinearLayout` node, replacing hello current content:</span></span>

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

