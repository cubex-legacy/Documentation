<a name="baseattribute"></a>
###Base Attribute

<a name="polymorphic"></a>
###Polymorphic Attributes

A Polymorphic attribute acts as a container for other mappers, within a single
attribute on your mapper.  If you wish to link a generic mapper onto another mapper
you can set and get from your attribute as if it were a standard data mapper,
with the added benefit of the data being stored in the database simply being the
class (type) of the external mapper and the id.  This will result in two columns
being created in your data source, based on the attribute name.  e.g.

  class Example extends DataMapper
  {
    public $child;
    public $name;

    protected function _configure()
    {
      $this->_addPolymorphicAttribute("child");
    }
  }

  $example = new Example(1);
  $example->name = "Parent";
  $example->child = new Example(2);
  $example->child->name = "Child";
  $example->child->saveChanges();
  $example->saveChanges();

  $loader = new Example(1);
  echo $loader->child->name; //Child

<a name="callback"></a>
###Callback Attributes

<a name="multributes"></a>
###Mutributes

<a name="composite"></a>
###Composite Attributes

<a name="compound"></a>
###Compound Attributes
