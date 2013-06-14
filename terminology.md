Cubex Terminology
==

###Mappers
Mappers are object representations of data sources, such as MySQL or cassandra.
Each mapper contains each column as a public property, and allows direct access
to the data source, giving you the ability to load, save & delete rows from your
data source.

###ViewModel
A view model offers a structured representation of your pages, with
TemplatedViewModels pre-loading a phtml template for you to push the data into.
Your view model should accept structured data from your controller, and either
build up the html within code, or handle the logic to ensure your templates are
kept very lean.
