<!-- default file list -->
*Files to look at*:

* [HomeController.cs](./CS/Controllers/HomeController.cs) (VB: [HomeController.vb](./VB/Controllers/HomeController.vb))
* [Global.asax.cs](./CS/Global.asax.cs) (VB: [Global.asax.vb](./VB/Global.asax.vb))
* [Product.cs](./CS/Models/Product.cs) (VB: [Product.vb](./VB/Models/Product.vb))
* [GridViewPartial.cshtml](./CS/Views/Home/GridViewPartial.cshtml)
* [Index.cshtml](./CS/Views/Home/Index.cshtml)
* [ProductFormPartial.cshtml](./CS/Views/Home/ProductFormPartial.cshtml)
<!-- default file list end -->
# OBSOLETE - How to enable unobtrusive validation for GridView using the EditForm template


<p>Starting with DevExpress 14.1, the ASP.NET MVC GridView extension fully supports the unobtrusive client validation for built-in edit forms. Refer to the <a href="https://www.devexpress.com/Support/Center/p/S173266">Support unobtrusive validation for the GridView's built-in edit form</a> thread to learn more.<br /><br />If you have version v14.1+ available, consider using the built-in functionality instead of the approach detailed below.<br />If you need further clarification, create a new ticket in our Support Center.<br /><br />The example illustrates how to implement unobtrusive validation for GridView editors. Create an Edit Form template that contains a form and all necessary editors. Corresponding validation attributes will be rendered for the template.<br /> The main requirement is that the updating should be performed using a helper script. In the script block, we prepare validation conditions and check them for the form (that is located within the Edit Form template). If all editors are valid, the grid's <strong>UpdateEdit</strong> command is invoked.</p>


```js
function UpdateGridView() {
   PrepareValidationScripts(); 
   var validator = $.data($('#frmProduct')[0], 'validator');
   if (validator.form())
       grid.UpdateEdit();
} 
function PrepareValidationScripts() {
   var form = $('#frmProduct');
   if (form.executed)
       return; 
   form.removeData("validator");
   $.validator.unobtrusive.parse(document);
   form.executed = true;
} 

```


<p><a href="https://www.devexpress.com/Support/Center/p/E3746">GridView - EditForm template - How to enable Microsoft MVC validation</a><u><br /> </u><a href="https://www.devexpress.com/Support/Center/p/E4924">GridView - How to perform a custom client side unobtrusive validation for the EditForm template using a custom attribute</a></p>


<h3>Description</h3>

<p>The <i>Global.asax</i> file contains a definition of the <strong>DefaultBinder</strong> property to provide an easy way to update custom models with DevExpress extensions.</p>

<br/>


