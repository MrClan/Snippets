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




#Creating a new section in Backoffice:

Part I : https://blogit.create.pt/andresantos/2015/11/30/building-an-umbraco-7-backoffice-extension-part-i/


Steps to add a new section:
___________________________________________

Step0: Create a new empty MVC application in visual studio and install Umbraco.Cms nuget package. Or, you may also continue with an existing Umbraco application.

Step1: Create a new .cs file that inherits from IApplication class inside umbraco.interfaces dll with the following code:

	[Application("ControlCenter", "ControlCenter", "icon-people", 15)]
    public class ControlCenterSection : IApplication
    {
        public ControlCenterSection()
        {

        }
    }
	
Step2: From inside Umbraco folder (which is hidden by default in the solution explorer), inside the Config/Lang folder, there is a file named "en.xml". Update the node with <area alias="sections"> and add the a new key like this: 
	<key alias="analytics">Analytics</key>
	
Step3: Build the application. Restart the application. Go to Users, and update permissions to show the newly created section.

Step4: Logout and re login. The newly created section should show.


Steps to remove the newly added section:
___________________________________________

Step0: Delete the row containing the new section name from Umbracouser2app table
Step1: Open the file config\applications.config and delete the line containing the new section name: 
	<add alias="ControlCenter" name="ControlCenter" icon="icon-people" sortOrder="15" />
	
NEXT: https://blogit.create.pt/andresantos/2015/11/30/building-an-umbraco-7-backoffice-extension-part-ii/
NEXT: https://blogit.create.pt/andresantos/2015/11/30/building-an-umbraco-7-backoffice-extension-part-iii/



