---
title: "Azure zarządzanych aplikacji przekazywaniem plików elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Common.FileUpload interfejsu użytkownika dla aplikacji Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="bcf0a-103">Element Microsoft.Common.FileUpload interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="bcf0a-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="bcf0a-104">Formant, który umożliwia użytkownikowi określenie co najmniej jeden plik do przekazania.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="bcf0a-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="bcf0a-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="bcf0a-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="bcf0a-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="bcf0a-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="bcf0a-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="bcf0a-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bcf0a-109">Remarks</span></span>
- <span data-ttu-id="bcf0a-110">`constraints.accept`Określa typy plików, które są wyświetlane w oknie dialogowym pliku przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="bcf0a-111">Zobacz [specyfikacji HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) dla dozwolone wartości.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="bcf0a-112">Wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-112">The default value is **null**.</span></span>
- <span data-ttu-id="bcf0a-113">Jeśli `options.multiple` ustawiono **true**, użytkownik może wybrać więcej niż jednego pliku w oknie dialogowym pliku przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="bcf0a-114">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-114">The default value is **false**.</span></span>
- <span data-ttu-id="bcf0a-115">Ten element obsługuje przekazywanie plików w dwóch trybach, w oparciu o wartości `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="bcf0a-116">Jeśli **pliku** jest określony, dane wyjściowe zawierają zawartość pliku jako obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="bcf0a-117">Jeśli **adres url** jest określona, plik jest przekazywany do tymczasowej lokalizacji, a dane wyjściowe zawierają adresu URL obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="bcf0a-118">Tymczasowe obiekty BLOB zostaną usunięte po 24 godzinach.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="bcf0a-119">Wartość domyślna to **pliku**.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-119">The default value is **file**.</span></span>
- <span data-ttu-id="bcf0a-120">Wartość `options.openMode` określa sposób odczytać pliku.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="bcf0a-121">Jeśli plik powinien być zwykłego tekstu, określ **tekst**; w przeciwnym razie, określ **binarne**.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="bcf0a-122">Wartość domyślna to **tekstu**.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-122">The default value is **text**.</span></span>
- <span data-ttu-id="bcf0a-123">Jeśli `options.uploadMode` ma ustawioną wartość **pliku** i `options.openMode` ustawiono **binarne**, dane wyjściowe są algorytmem Base64.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="bcf0a-124">`options.encoding`Określa kodowanie używane podczas odczytu pliku.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="bcf0a-125">Wartość domyślna to **UTF-8**i jest używany tylko wtedy, gdy `options.openMode` ustawiono **tekstu**.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="bcf0a-126">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="bcf0a-126">Sample output</span></span>
<span data-ttu-id="bcf0a-127">Jeśli options.uploadMode jest plikiem options.multiple ma wartość false, następnie dane wyjściowe zawierają zawartość pliku jako ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="bcf0a-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="bcf0a-128">Jeśli options.multiple ma wartość true and'options.uploadMode pliku, wówczas dane wyjściowe zawierają zawartość plików w postaci tablicy JSON:</span><span class="sxs-lookup"><span data-stu-id="bcf0a-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="bcf0a-129">Jeśli adres url jest options.uploadMode options.multiple ma wartość false, następnie dane wyjściowe zawiera adres URL jako ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="bcf0a-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="bcf0a-130">Jeśli adres url jest options.uploadMode options.multiple ma wartość true, następnie dane wyjściowe zawierają listę adresów URL jako tablica JSON:</span><span class="sxs-lookup"><span data-stu-id="bcf0a-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="bcf0a-131">Podczas testowania CreateUiDefinition, niektóre przeglądarki (np. Google Chrome) obciąć adresy URL wygenerowanym przez dany element Microsoft.Common.FileUpload w konsoli przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="bcf0a-132">Konieczne może być kliknij prawym przyciskiem myszy poszczególnych łączy do skopiowania pełne adresy URL.</span><span class="sxs-lookup"><span data-stu-id="bcf0a-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bcf0a-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bcf0a-133">Next steps</span></span>
* <span data-ttu-id="bcf0a-134">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcf0a-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="bcf0a-135">Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcf0a-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="bcf0a-136">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="bcf0a-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
