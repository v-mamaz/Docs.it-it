---
title: Helper tag Partial in ASP.NET Core
author: scottaddie
description: Informazioni sull'helper tag Partial di ASP.NET Core e sul ruolo dei singoli attributi dell'helper nel rendering di una visualizzazione parziale.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 04/13/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/partial-tag-helper
ms.openlocfilehash: 786c333980db89a9a5a60dc70c0bd1998ca159cd
ms.sourcegitcommit: 74be78285ea88772e7dad112f80146b6ed00e53e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/10/2018
---
# <a name="partial-tag-helper-in-aspnet-core"></a><span data-ttu-id="da4cc-103">Helper tag Partial in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="da4cc-103">Partial Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="da4cc-104">Di [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="da4cc-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="da4cc-105">[Visualizzare o scaricare il codice di esempio](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples) ([procedura per il download](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="da4cc-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/tag-helpers/built-in/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="overview"></a><span data-ttu-id="da4cc-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="da4cc-106">Overview</span></span>

<span data-ttu-id="da4cc-107">L'helper tag Partial viene usato per il rendering di una [visualizzazione parziale](xref:mvc/views/partial) in Razor Pages e nelle app MVC.</span><span class="sxs-lookup"><span data-stu-id="da4cc-107">The Partial Tag Helper is used for rendering a [partial view](xref:mvc/views/partial) in Razor Pages and MVC apps.</span></span> <span data-ttu-id="da4cc-108">Tenere presente che:</span><span class="sxs-lookup"><span data-stu-id="da4cc-108">Consider that it:</span></span>

* <span data-ttu-id="da4cc-109">Richiede ASP.NET Core 2.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="da4cc-109">Requires ASP.NET Core 2.1 or later.</span></span>
* <span data-ttu-id="da4cc-110">Rappresenta un'alternativa alla [sintassi helper HTML](xref:mvc/views/partial#referencing-a-partial-view).</span><span class="sxs-lookup"><span data-stu-id="da4cc-110">Is an alternative to [HTML Helper syntax](xref:mvc/views/partial#referencing-a-partial-view).</span></span>
* <span data-ttu-id="da4cc-111">Esegue il rendering della visualizzazione parziale in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="da4cc-111">Renders the partial view asynchronously.</span></span>

<span data-ttu-id="da4cc-112">Le opzioni helper HTML per il rendering di una visualizzazione parziale includono:</span><span class="sxs-lookup"><span data-stu-id="da4cc-112">The HTML Helper options for rendering a partial view include:</span></span>

* [<span data-ttu-id="da4cc-113">@await Html.PartialAsync</span><span class="sxs-lookup"><span data-stu-id="da4cc-113">@await Html.PartialAsync</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partialasync)
* [<span data-ttu-id="da4cc-114">@await Html.RenderPartialAsync</span><span class="sxs-lookup"><span data-stu-id="da4cc-114">@await Html.RenderPartialAsync</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartialasync)
* [@Html.Partial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partial)
* [@Html.RenderPartial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartial)

<span data-ttu-id="da4cc-115">Il modello *Product* è usato negli esempi di questo documento:</span><span class="sxs-lookup"><span data-stu-id="da4cc-115">The *Product* model is used in samples throughout this document:</span></span>

[!code-csharp[](samples/TagHelpersBuiltIn/Models/Product.cs)]

<span data-ttu-id="da4cc-116">Segue un inventario degli attributi dell'helper tag Partial.</span><span class="sxs-lookup"><span data-stu-id="da4cc-116">An inventory of the Partial Tag Helper attributes follows.</span></span>

## <a name="name"></a><span data-ttu-id="da4cc-117">name</span><span class="sxs-lookup"><span data-stu-id="da4cc-117">name</span></span>

<span data-ttu-id="da4cc-118">L'attributo `name` è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="da4cc-118">The `name` attribute is required.</span></span> <span data-ttu-id="da4cc-119">Indica il nome o il percorso della visualizzazione parziale di cui eseguire il rendering.</span><span class="sxs-lookup"><span data-stu-id="da4cc-119">It indicates the name or the path of the partial view to be rendered.</span></span> <span data-ttu-id="da4cc-120">Quando viene offerto un nome della visualizzazione parziale, viene avviato il processo di [individuazione delle visualizzazioni](xref:mvc/views/overview#view-discovery).</span><span class="sxs-lookup"><span data-stu-id="da4cc-120">When a partial view name is provided, the [view discovery](xref:mvc/views/overview#view-discovery) process is initiated.</span></span> <span data-ttu-id="da4cc-121">Tale processo viene ignorato quando viene offerto un percorso esplicito.</span><span class="sxs-lookup"><span data-stu-id="da4cc-121">That process is bypassed when an explicit path is provided.</span></span>

<span data-ttu-id="da4cc-122">Il markup seguente usa un percorso esplicito, che indica che *_ProductPartial.cshtml* deve essere caricato dalla cartella *Shared*.</span><span class="sxs-lookup"><span data-stu-id="da4cc-122">The following markup uses an explicit path, indicating that *_ProductPartial.cshtml* is to be loaded from the *Shared* folder.</span></span> <span data-ttu-id="da4cc-123">Mediante l'attributo [for](#for) un modello viene passato alla visualizzazione parziale per l'associazione.</span><span class="sxs-lookup"><span data-stu-id="da4cc-123">Using the [for](#for) attribute, a model is passed to the partial view for binding.</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Name)]

## <a name="for"></a><span data-ttu-id="da4cc-124">for</span><span class="sxs-lookup"><span data-stu-id="da4cc-124">for</span></span>

<span data-ttu-id="da4cc-125">L'attributo `for` assegna una [ModelExpression](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.modelexpression) da valutare rispetto al modello corrente.</span><span class="sxs-lookup"><span data-stu-id="da4cc-125">The `for` attribute assigns a [ModelExpression](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.modelexpression) to be evaluated against the current model.</span></span> <span data-ttu-id="da4cc-126">Un elemento `ModelExpression` deduce la sintassi `@Model.`.</span><span class="sxs-lookup"><span data-stu-id="da4cc-126">A `ModelExpression` infers the `@Model.` syntax.</span></span> <span data-ttu-id="da4cc-127">Ad esempio `for="Product"` può essere usato invece di `for="@Model.Product"`.</span><span class="sxs-lookup"><span data-stu-id="da4cc-127">For example, `for="Product"` can be used instead of `for="@Model.Product"`.</span></span> <span data-ttu-id="da4cc-128">Questo comportamento di inferenza predefinito può essere ignorato se si usa il simbolo `@` per definire un'espressione inline.</span><span class="sxs-lookup"><span data-stu-id="da4cc-128">This default inference behavior is overridden by using the `@` symbol to define an inline expression.</span></span> <span data-ttu-id="da4cc-129">L'attributo `for` non può essere usato con l'attributo [model](#model).</span><span class="sxs-lookup"><span data-stu-id="da4cc-129">The `for` attribute can't be used with the [model](#model) attribute.</span></span>

<span data-ttu-id="da4cc-130">Il markup seguente carica *_ProductPartial.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="da4cc-130">The following markup loads *_ProductPartial.cshtml*:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_For)]

<span data-ttu-id="da4cc-131">La visualizzazione parziale è correlata alla proprietà `Product` del modello di pagina associato:</span><span class="sxs-lookup"><span data-stu-id="da4cc-131">The partial view is bound to the associated page model's `Product` property:</span></span>

[!code-csharp[](samples/TagHelpersBuiltIn/Pages/Product.cshtml.cs?highlight=8)]

## <a name="model"></a><span data-ttu-id="da4cc-132">modello</span><span class="sxs-lookup"><span data-stu-id="da4cc-132">model</span></span>

<span data-ttu-id="da4cc-133">L'attributo `model` assegna un'istanza del modello da passare alla visualizzazione parziale.</span><span class="sxs-lookup"><span data-stu-id="da4cc-133">The `model` attribute assigns a model instance to pass to the partial view.</span></span> <span data-ttu-id="da4cc-134">L'attributo `model` non può essere usato con l'attributo [for](#for).</span><span class="sxs-lookup"><span data-stu-id="da4cc-134">The `model` attribute can't be used with the [for](#for) attribute.</span></span>

<span data-ttu-id="da4cc-135">Nel markup seguente viene creata un'istanza di un nuovo oggetto `Product` che viene quindi passata all'attributo `model` per il binding:</span><span class="sxs-lookup"><span data-stu-id="da4cc-135">In the following markup, a new `Product` object is instantiated and passed to the `model` attribute for binding:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_Model)]

## <a name="view-data"></a><span data-ttu-id="da4cc-136">view-data</span><span class="sxs-lookup"><span data-stu-id="da4cc-136">view-data</span></span>

<span data-ttu-id="da4cc-137">L'attributo `view-data` assegna un [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) da passare alla visualizzazione parziale.</span><span class="sxs-lookup"><span data-stu-id="da4cc-137">The `view-data` attribute assigns a [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) to pass to the partial view.</span></span> <span data-ttu-id="da4cc-138">Il markup seguente rende l'intera raccolta ViewData accessibile alla visualizzazione parziale:</span><span class="sxs-lookup"><span data-stu-id="da4cc-138">The following markup makes the entire ViewData collection accessible to the partial view:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Product.cshtml?name=snippet_ViewData&highlight=5-)]

<span data-ttu-id="da4cc-139">Nel codice precedente, il valore della chiave `IsNumberReadOnly` è impostato su `true` e aggiunto alla raccolta ViewData.</span><span class="sxs-lookup"><span data-stu-id="da4cc-139">In the preceding code, the `IsNumberReadOnly` key value is set to `true` and added to the ViewData collection.</span></span> <span data-ttu-id="da4cc-140">Di conseguenza l'elemento `ViewData["IsNumberReadOnly"]` viene reso accessibile all'interno della visualizzazione parziale seguente:</span><span class="sxs-lookup"><span data-stu-id="da4cc-140">Consequently, `ViewData["IsNumberReadOnly"]` is made accessible within the following partial view:</span></span>

[!code-cshtml[](samples/TagHelpersBuiltIn/Pages/Shared/_ProductViewDataPartial.cshtml?highlight=5)]

<span data-ttu-id="da4cc-141">In questo esempio il valore di `ViewData["IsNumberReadOnly"]` determina se il campo *Number* viene visualizzato come campo di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="da4cc-141">In this example, the value of `ViewData["IsNumberReadOnly"]` determines whether the *Number* field is displayed as read only.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="da4cc-142">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="da4cc-142">Additional resources</span></span>

* [<span data-ttu-id="da4cc-143">Visualizzazioni parziali</span><span class="sxs-lookup"><span data-stu-id="da4cc-143">Partial views</span></span>](xref:mvc/views/partial)
* [<span data-ttu-id="da4cc-144">Dati con tipizzazione debole (ViewData, attributo ViewData e ViewBag)</span><span class="sxs-lookup"><span data-stu-id="da4cc-144">Weakly typed data (ViewData, ViewData attribute, and ViewBag)</span></span>](xref:mvc/views/overview#weakly-typed-data-viewdata-viewdata-attribute-and-viewbag)