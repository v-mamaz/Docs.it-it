<!--
[!code-html[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/_Layout.cshtml?highlight=7,31)]


[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull)]

![Index view](../../tutorials/first-mvc-app/search/_static/ghost.png)


[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]

--> 

<span data-ttu-id="0b718-101">Il metodo `Index` precedente:</span><span class="sxs-lookup"><span data-stu-id="0b718-101">The previous `Index` method:</span></span>

<span data-ttu-id="0b718-102">[!code-csharp[Principale](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_1stSearch)]</span><span class="sxs-lookup"><span data-stu-id="0b718-102">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_1stSearch)]</span></span>

<span data-ttu-id="0b718-103">Il metodo `Index` aggiornato con il parametro `id`:</span><span class="sxs-lookup"><span data-stu-id="0b718-103">The updated `Index` method with `id` parameter:</span></span>

<span data-ttu-id="0b718-104">[!code-csharp[Principale](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_SearchID)]</span><span class="sxs-lookup"><span data-stu-id="0b718-104">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_SearchID)]</span></span>

<span data-ttu-id="0b718-105">È ora possibile passare il titolo della ricerca come dati di route (un segmento di URL), anziché come valore della stringa di query.</span><span class="sxs-lookup"><span data-stu-id="0b718-105">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![Vista Index con la parola ghost aggiunta all'URL e un elenco restituito di due film: Ghostbusters e Ghostbusters 2](../../tutorials/first-mvc-app/search/_static/g2.png)

<span data-ttu-id="0b718-107">Tuttavia, non è possibile supporre che gli utenti modifichino l'URL ogni volta che desiderano cercare un film.</span><span class="sxs-lookup"><span data-stu-id="0b718-107">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="0b718-108">A questo punto si aggiungerà l'interfaccia utente per filtrare i film.</span><span class="sxs-lookup"><span data-stu-id="0b718-108">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="0b718-109">Se è stata modificata la firma del metodo `Index` per testare come passare il parametro `ID` associato alla route, impostarlo di nuovo in modo che accetti un parametro denominato `searchString`:</span><span class="sxs-lookup"><span data-stu-id="0b718-109">If you changed the signature of the `Index` method to test how to pass the route-bound `ID` parameter, change it back so that it takes a parameter named `searchString`:</span></span>

<span data-ttu-id="0b718-110">[!code-csharp[Principale](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_1stSearch)]</span><span class="sxs-lookup"><span data-stu-id="0b718-110">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_1stSearch)]</span></span>

<span data-ttu-id="0b718-111">Aprire il file *Views/Movies/Index.cshtml* e aggiungere il markup `<form>` evidenziato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0b718-111">Open the *Views/Movies/Index.cshtml* file, and add the `<form>` markup highlighted below:</span></span>

<span data-ttu-id="0b718-112">[!code-HTML[Principale](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexForm1.cshtml?highlight=10-16&range=4-21)]</span><span class="sxs-lookup"><span data-stu-id="0b718-112">[!code-HTML[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexForm1.cshtml?highlight=10-16&range=4-21)]</span></span>

<span data-ttu-id="0b718-113">Il tag `<form>` HTML usa l'[helper tag del modulo](../../mvc/views/working-with-forms.md) e quindi quando si invia il modulo, la stringa di filtro viene registrata nell'azione `Index` del controller di film.</span><span class="sxs-lookup"><span data-stu-id="0b718-113">The HTML `<form>` tag uses the [Form Tag Helper](../../mvc/views/working-with-forms.md), so when you submit the form, the filter string is posted to the `Index` action of the movies controller.</span></span> <span data-ttu-id="0b718-114">Salvare le modifiche e quindi testare il filtro.</span><span class="sxs-lookup"><span data-stu-id="0b718-114">Save your changes and then test the filter.</span></span>

![Vista Index con la parola ghost digitata nella casella di testo del filtro del titolo](../../tutorials/first-mvc-app/search/_static/filter.png)

<span data-ttu-id="0b718-116">Non è presente alcun overload del metodo `[HttpPost]` `Index` come previsto.</span><span class="sxs-lookup"><span data-stu-id="0b718-116">There's no `[HttpPost]` overload of the `Index` method as you might expect.</span></span> <span data-ttu-id="0b718-117">Non è necessario perché il metodo non modifica lo stato dell'app, ma filtra solo i dati.</span><span class="sxs-lookup"><span data-stu-id="0b718-117">You don't need it, because the method isn't changing the state of the app, just filtering data.</span></span>

<span data-ttu-id="0b718-118">È possibile aggiungere il metodo `[HttpPost] Index` seguente.</span><span class="sxs-lookup"><span data-stu-id="0b718-118">You could add the following `[HttpPost] Index` method.</span></span>

<span data-ttu-id="0b718-119">[!code-csharp[Principale](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_SearchPost)]</span><span class="sxs-lookup"><span data-stu-id="0b718-119">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_SearchPost)]</span></span>

<span data-ttu-id="0b718-120">Il parametro `notUsed` viene usato per creare un overload per il metodo `Index`.</span><span class="sxs-lookup"><span data-stu-id="0b718-120">The `notUsed` parameter is used to create an overload for the `Index` method.</span></span> <span data-ttu-id="0b718-121">Questo aspetto verrà trattato in una fase successiva dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0b718-121">We'll talk about that later in the tutorial.</span></span>

<span data-ttu-id="0b718-122">Se si aggiunge questo metodo, l'invoker di azione trova la corrispondenza con il metodo `[HttpPost] Index` e il metodo `[HttpPost] Index` viene eseguito come illustrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="0b718-122">If you add this method, the action invoker would match the `[HttpPost] Index` method, and the `[HttpPost] Index` method would run as shown in the image below.</span></span>

![Finestra del browser con la risposta dell'applicazione From HttpPost Index: filter on ghost](../../tutorials/first-mvc-app/search/_static/fo.png)

<span data-ttu-id="0b718-124">Tuttavia, anche se si aggiunge questa versione `[HttpPost]` del metodo `Index`, esiste una limitazione sul modo sulla relativa implementazione.</span><span class="sxs-lookup"><span data-stu-id="0b718-124">However, even if you add this `[HttpPost]` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="0b718-125">Si supponga che si desideri usare come segnalibro una ricerca specifica o inviare un collegamento agli amici su cui possono fare clic per visualizzare lo stesso elenco filtrato di film.</span><span class="sxs-lookup"><span data-stu-id="0b718-125">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="0b718-126">Si noti che l'URL per la richiesta HTTP POST è lo stesso URL per la richiesta GET (localhost:xxxxx/Movies/Index); le informazioni sulla ricerca non sono disponibili nell'URL.</span><span class="sxs-lookup"><span data-stu-id="0b718-126">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL.</span></span> <span data-ttu-id="0b718-127">Le informazioni sulla stringa di ricerca vengono inviate al server come un [valore del campo modulo](https://developer.mozilla.org/docs/Web/Guide/HTML/Forms/Sending_and_retrieving_form_data).</span><span class="sxs-lookup"><span data-stu-id="0b718-127">The search string information is sent to the server as a [form field value](https://developer.mozilla.org/docs/Web/Guide/HTML/Forms/Sending_and_retrieving_form_data).</span></span> <span data-ttu-id="0b718-128">È possibile eseguire una verifica con gli strumenti di sviluppo del browser o l'eccellente [strumento Fiddler](http://www.telerik.com/fiddler).</span><span class="sxs-lookup"><span data-stu-id="0b718-128">You can verify that with the browser Developer tools or the excellent [Fiddler tool](http://www.telerik.com/fiddler).</span></span> <span data-ttu-id="0b718-129">L'immagine seguente mostra gli strumenti di sviluppo del browser Chrome:</span><span class="sxs-lookup"><span data-stu-id="0b718-129">The image below shows the Chrome browser Developer tools:</span></span>

![Scheda di rete degli strumenti di sviluppo in Microsoft Edge che mostra il corpo di una richiesta con un valore searchString di ghost](../../tutorials/first-mvc-app/search/_static/f12_rb.png)

<span data-ttu-id="0b718-131">È possibile esaminare il parametro di ricerca e il token [XSRF](../../security/anti-request-forgery.md) nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="0b718-131">You can see the search parameter and [XSRF](../../security/anti-request-forgery.md) token in the request body.</span></span> <span data-ttu-id="0b718-132">Si noti, come indicato nell'esercitazione precedente, che l'[helper tag del modulo](../../mvc/views/working-with-forms.md) genera un token antifalsificazione [XSRF](../../security/anti-request-forgery.md).</span><span class="sxs-lookup"><span data-stu-id="0b718-132">Note, as mentioned in the previous tutorial, the [Form Tag Helper](../../mvc/views/working-with-forms.md) generates an [XSRF](../../security/anti-request-forgery.md) anti-forgery token.</span></span> <span data-ttu-id="0b718-133">Poiché non si stanno modificando i dati, non è necessario convalidare il token nel metodo del controller.</span><span class="sxs-lookup"><span data-stu-id="0b718-133">We're not modifying data, so we don't need to validate the token in the controller method.</span></span>

<span data-ttu-id="0b718-134">Poiché il parametro di ricerca si trova nel corpo della richiesta e non nell'URL, non è possibile acquisire queste informazioni sulla ricerca da usare come segnalibro o condividerle con altri utenti.</span><span class="sxs-lookup"><span data-stu-id="0b718-134">Because the search parameter is in the request body and not the URL, you can't capture that search information to bookmark or share with others.</span></span> <span data-ttu-id="0b718-135">È possibile risolvere il problema specificando che la richiesta deve essere `HTTP GET`.</span><span class="sxs-lookup"><span data-stu-id="0b718-135">We'll fix this by specifying the request should be `HTTP GET`.</span></span>