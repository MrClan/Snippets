Notes:

1. To redirect to another page, use umbraco internal property called **umbracoInternalRedirectId**
2. To get all the child pages, as TypedContent, use: **Umbraco.TypedContentAtRoot().First().Children**
3. To get url of a document by Id, use: **Umbraco.NiceUrl(id)**



####Doc link: 
[RenderModel](https://our.umbraco.org/apidocs/csharp/api/Umbraco.Web.Models.RenderModel.html)


####Dumps all properties of all document types under root:

```cshtml
<hr/>
	<ul>
		@{
		var r= Model.Content.Parent;
		<b>Type = @r.GetType()</b>
		foreach (var s in r.Children)
		{
			try
			{
			<li>
				@(s.Name)
				<ul>
					@{
					<b>Type = @s.GetType()</b>
					foreach (var p in s.GetType().GetProperties())
					{
						try
						{
						<li>@(p.Name + "  ->  " + p.GetValue(s, null))</li>
						}catch
						{
							<li>Exception for: @p.Name</li>
						}

					}}
				</ul>
			</li>
				
			}catch
			{
				<li>Exception for: @s.Name</li>
			}

		}}
	</ul>
<hr/>
````

####To redirect a link to some other page
** The documentType contains two properties of the type "contentPicker" and their aliases are umbracoRedirect and umbracoInternalRedirectId. Once you pick a page, the redirecting will be done automagically by Umbraco.**
